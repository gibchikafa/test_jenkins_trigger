node("local") {
  def downstreamJobName = env.DLT_JOB_NAME ?: "k8s-dlt"
  def upstreamBranch = env.BRANCH_NAME ?: "main"
  def downstreamJob = downstreamJobName
  def dltImageVersion = env.DLT_IMAGE_VERSION ?: "test-SNAPSHOT"
  def baseImageVersion = env.BASE_IMAGE_VERSION ?: "5.0.0-SNAPSHOT"

  stage('Checkout') {
    checkout scm
  }

  stage('Dummy upstream work') {
    echo "Trigger test job running from branch: ${upstreamBranch}"
    echo "Configured downstream job: ${downstreamJob}"
    echo "Passing DLT_GIT_BRANCH=${upstreamBranch}"
    echo "Passing DLT_IMAGE_VERSION=${dltImageVersion}"
    echo "Passing BASE_IMAGE_VERSION=${baseImageVersion}"
  }

  stage('Trigger hopsworks-dlt') {
    build job: downstreamJob,
      wait: false,
      propagate: false,
      parameters: [
        string(name: 'DLT_GIT_BRANCH', value: "autosync_base_image_with_hopsworks"),
        string(name: 'DLT_IMAGE_VERSION', value: dltImageVersion),
        string(name: 'BASE_IMAGE_VERSION', value: baseImageVersion)
      ]
  }
}
