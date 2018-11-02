node {
  def label_repo
  def label_tag
  def label

  try {
    stage('Clone repository') { checkout scm }

    stage('Build image') {
      def uuid = UUID.randomUUID().toString()
      label_repo = "wait-for_ci_runs"
      label_tag = "build_${uuid}"
      label = "${label_repo}:${label_tag}"

      docker.build(label, ".")
    }

    stage('Run tests') {
      sh "docker run --rm ${label}"
    }
  } finally {
    stage('Cleanup') {
      cleanupTestContainers(label_repo)
    }
  }
}
