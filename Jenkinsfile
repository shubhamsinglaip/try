pipeline

{

    agent any

    stages

    {

        stage('stage 1')

        {

           agent

            {

                label 'myfirstagent'

            }

            steps

            {

                sh'git init'

                sh'rm -rf first'

                sh'git clone https://github.com/apoorvasahu25/first.git'

                sh 'echo "multi-node-demo-1"'

                stash(name: 'source')

            }

        }

        stage('stage 2')

        {

            agent

            {

                label 'jennode'

            }

            steps

            {

                sh 'echo "multi-node-demo-2"'

                unstash(name: 'source')

                sh'pwd'

                sh'cd first/'

                

                sh 'chmod 777 first/script.sh'

                

                sh'./first/script.sh'

            }

        }

    }

}
