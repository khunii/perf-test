pipeline{
    agent any
    environment{
        Thread_Group='100'
        Ramp_Up = '50'
    }

    stages{
        stage('Clone Test'){
            steps{
                git branch: 'main', url: 'https://github.com/khunii/perf-test.git'
            }
        }
        stage('execute test'){
            steps{
                sh "/usr/local/bin/jmeter -Jjmeter.save.saveservice.output_format=xml \
                -JThreadGroup=${env.Thread_Group} -JRampUp=${env.Ramp_Up} \
                -n -t script/first.jmx -l report/first_${env.BUILD_NUMBER}.jtl"
            }
        }
        stage('report test'){
            steps{
                perfReport showTrendGraphs: true, sourceDataFiles: "report/first_${env.BUILD_NUMBER}.jtl"
                archiveArtifacts '**/*.jtl, **/jmeter.log'
            }
        }
    }
}