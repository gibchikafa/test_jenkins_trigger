node("local") {
  def downstreamJobName = env.DLT_JOB_NAME ?: "k8s-dlt"
  def upstreamBranch = env.BRANCH_NAME ?: "main"
  def downstreamBranch = env.DLT_JOB_BRANCH?.trim()
  def downstreamJob = downstreamBranch ? "${downstreamJobName}/${downstreamBranch}" : downstreamJobName
  def baseImage = env.BASE_IMAGE ?: "docker.hops.works/hopsworks/hopsworks-base:pandas-training-pipeline-test"

  stage('Checkout') {
    checkout scm
  }

  stage('Dummy upstream work') {
    echo "Trigger test job running from branch: ${upstreamBranch}"
    echo "Configured downstream job: ${downstreamJob}"
    echo "Passing BASE_IMAGE=${baseImage}"
  }

  stage('Trigger hopsworks-dlt') {
    build job: downstreamJob,
      wait: false,
      propagate: false,
      parameters: [
        string(name: 'BASE_IMAGE', value: baseImage)
      ]
  }
}
