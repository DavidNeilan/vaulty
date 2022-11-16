pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh '''#!/bin/bash
                    /usr/bin/git submodule update --init --recursive && pushd vaultwarden
                    cargo clean && cargo build --features sqlite --release
                    file target/release/vaultwarden

                    pushd target/release/
                    /usr/bin/git clone https://github.com/bitwarden/web.git web-vault.git && cd web-vault.git
                    /usr/bin/git checkout v2.11
                    /usr/bin/git apply v2.11.0.patch
                    npm run sub:init && npm install && npm run dist
                    cp -a build ../web-vault

                '''
            }
        }
    }
}