node {
    checkout scm

    generalPipeline{
        if (env.BRANCH_NAME == 'main') {
            prodBuild()
        } else {
            prBuild()
        }
    }
}


def prBuild() {

    def meuseImage

    jenkinsImage = buildImage(product: 'kenbun', name: 'meuse', commandlineOptions: ' -f Dockerfile')
    test(image: meuseImage)

    return meuseImage
}


def prodBuild() {

    meuseImage = prBuild()

    scanImage(product: 'kenbun', name: 'meuse', dockerfile:'Dockerfile')
    pushToRegistry(image: meuseImage)
}
