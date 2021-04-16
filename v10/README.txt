Build
    docker build -t private/cordova-10 .

Interactive
    docker run --rm -ti -w /workspace -v "HOST_PATH:/workspace" private/cordova-10 bash
