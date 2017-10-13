pipeline {
  agent any
  stages {
    stage('Pull down config files') {
      steps {
        echo 'Grabbing Config Files from server'
        sh '''# scp s27app:~/fpcConfigTest/fpcConfigTest.tgz . || echo "archive not found... proceeding"

echo "archive not found... proceeding"
'''
      }
    }
    stage('Execute Testcase Too') {
      steps {
        sh '''echo "=========================================================="
echo "[###] Execute testcase on remote appliance (via SSH) [###]"
echo "=========================================================="

ssh s27app "cd /root/fpcConfigTest; ./test_vlan_position_in_fpcConfig_file.sh"
'''
      }
    }
    stage('Collect Output Files') {
      steps {
        ws(dir: 'TestOutputFiles') {
          sh '''echo "==================================================="
echo "[###] The test generates some output files.         "
echo "      Zip them up and copy them to workspace: [###]"
echo "==================================================="

ssh s27app "cd /root/fpcConfigTest/test_results; tar -cvf ../fpc_config_test_results.tgz ."

scp s27app:/root/fpcConfigTest/fpc_config_test_results.tgz .
'''
          sh '''# Extract files from the archive
tar -xvf fpc_config_test_results.tgz'''
        }
        
      }
    }
    stage('DONE') {
      steps {
        echo 'Process Complete'
      }
    }
  }
}