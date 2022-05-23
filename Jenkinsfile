pipeline{
    environment{
        Thread_Group='100'
        Ramp_Up = '50'
        Loop_Count = '1'
    }

    stages{
        stage('Clone Test'){
            steps{
                git branch: 'main', url: 'https://github.com/khunii/perf-test.git'
            }
        }
        stage('execute test'){
            steps{
                sh "jmeter -Jjmeter.save.saveservice.output_format=xml \
                -JThreadGroup=${env.Thread_Group} -JRampUp=${env.Ramp_Up} \
                -JLoopCount=${env.Loop_Count} \
                -n -t script/first.jmx -l report/first.jtl"
            }
        }
        stage('report test'){
            steps{
                perfReport "report/first.jtl"
            }
        }
    }
}