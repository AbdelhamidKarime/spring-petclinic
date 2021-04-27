pipeline { 

    agent any 

    triggers { 
        pollSCM '* * * * *' 
    } 

    stages { 
        stage('GIT') { 
            steps { 
                // Get some code from a GitHub repository 
                git url: 'https://github.com/MEDAYOUBIDRISSI/spring-petclinic.git',branch:'devops1' 
            } 
            post{ 
                success{ 
                    echo 'Succès' 
                } 
                failure{ 
                    echo 'Echec' 
                } 
            } 
            } 
        stage ('BUILD'){ 
            steps { 
                sh "./mvnw clean compile" 
            } 
            post{ 
                success { 
                    echo 'Build réussi' 
                } 
            } 
        } 
        stage ('TEST'){ 
            steps { 
                sh "./mvnw test" 
            } 
            post{ 
                success { 
                  junit '**/target/surefire-reports/TEST-*.xml' 
                } 
            }
        }
        stage ('PACKAGE'){ 
            steps { 
                sh "./mvnw package" 
            } 
            post{ 
                success { 
                    archiveArtifacts artifacts: 'target/*.jar' 
                } 
            } 
        } 
       
    }
}
