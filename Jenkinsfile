@Library("plextools") import tv.plex.PlexTools

def tools = new PlexTools(this)
def dockerImage = 'plex/build-cloud:latest'

node('plex-linux-x86_64') {
  tools.docker(dockerImage) {
    stage('Checkout') {
      checkout(tools.checkout_obj())
    }

    stage('Install node modules') {
      tools.yarn_install(false)
    }

    def tag = env.TAG_NAME
    if (tag) {
      stage('Deploying…') {
        tools.publish_node_package()
      }
    }
  }
}
