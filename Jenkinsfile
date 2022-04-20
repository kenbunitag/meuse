node {
    checkout scm

    generalPipeline{
        if (env.BRANCH_NAME == 'master') {
            prodBuild()
        } else {
            prBuild()
        }
    }
}


def prBuild() {

    def meuseImage

    meuseImage = buildImage(product: 'kenbun', name: 'meuse', commandlineOptions: ' -f Dockerfile')
    test(image: meuseImage)

    return meuseImage
}


def prodBuild() {

    meuseImage = prBuild()

    scanImage(product: 'kenbun', name: 'meuse', dockerfile:'Dockerfile')
    pushToRegistry(image: meuseImage)
}
