node("local") {
  def downstreamJobRoot = env.DLT_JOB_NAME ?: "k8s-dlt"
  def upstreamBranch = env.BRANCH_NAME ?: "main"
  def downstreamBranch = upstreamBranch == "main" ? "master" : upstreamBranch
  def downstreamJob = "${downstreamJobRoot}/${downstreamBranch}"
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
      wait: true,
      propagate: true,
      parameters: [
        string(name: 'BASE_IMAGE', value: baseImage)
      ]
  }
}
