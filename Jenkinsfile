pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                sh '''#!/bin/bash
                    git submodule update --init --recursive && pushd
                    bitwarden_rs && cargo clean && cargo build --features sqlite --release
                    file target/release/bitwarden_rs
                '''
            }
        }
    }
}