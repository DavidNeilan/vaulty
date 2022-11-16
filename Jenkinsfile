pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh '''#!/bin/bash
                    git submodule update --init --recursive && pushd vaultwarden
                    cargo clean && cargo build --features sqlite --release
                    file target/release/vaultwarden

                    pushd target/release/
                    git clone git clone https://github.com/bitwarden/web.git web-vault.git && cd web-vault.git
                    git checkout v2.11
                    git apply v2.11.0.patch
                    npm run sub:init && npm install && npm run dist
                    cp -a build ../web-vault

                '''
            }
        }
    }
}