pipeline{
    agent any
    environment{
        Thread_Group='100'
        Ramp_Up = '50'
    }

    stages{
        stage('Clone Test'){
            steps{
                //git branch: 'main', url: 'https://github.com/khunii/perf-test.git'
                git url:'https://github.com/khunii/perf-test.git'
            }
        }
        stage('execute test'){
            steps{
                sh "/usr/local/bin/jmeter -J jmeter.save.saveservice.output_format=xml \
                -JThreadGroup=${env.Thread_Group} -JRampUp=${env.Ramp_Up} \
                -n -t ./script/sprint-test.jmx -l ./report/sprint_result_${env.BUILD_NUMBER}.jtl"
                //---
                // sh "/usr/local/bin/jmeter -J jmeter.save.saveservice.output_format=xml \
                // -n -t ./script/sprint-test.jmx -l ./report/sprint_result_${env.BUILD_NUMBER}.jtl"
                //---
                // sh "/usr/local/bin/jmeter \
                // -n -t ./script/sprint-test.jmx -l ./report/sprint_result_${env.BUILD_NUMBER}.jtl"
                //---
                //sh "/usr/local/bin/jmeter -n -t ./script/sprint-test.jmx -l logfile.jtl -e -o ./report/sprint_result_${env.BUILD_NUMBER}.jtl"


            }
        }
        stage('report test'){
            steps{
                perfReport filterRegex:'', showTrendGraphs: true, sourceDataFiles: "report/sprint_result_${env.BUILD_NUMBER}.jtl"
                archiveArtifacts '**/*.jtl, **/jmeter.log'
            }
        }
    }
}