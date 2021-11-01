# Collect Core Dumps From Containerized Apps with GitHub Actions

This repo demonstrates how to collect core dumps from an app running within a docker container using GitHub Actions.

[![Collect Core Dump](https://github.com/seladb/GHActionsCoreDumpCollect/actions/workflows/collect_core_dump.yml/badge.svg?branch=master)](https://github.com/seladb/GHActionsCoreDumpCollect/actions/workflows/collect_core_dump.yml)

In order to be able to collect the core dump a few steps are required:
- Run the container with elevated permissions and set the core dump size to unlimited: `options: --privileged --ulimit core=-1`
- When the container is running: define the location and the filename pattern of the core dump: `sysctl -w kernel.core_pattern="/tmp/core.%t.%e.%p"`
- Use the `upload-artifact` action to collect the core dump and the executable in the case of a failure

This repo includes:
- A very simple C program (under `src/`) that calls `abort()` to cause a core dump
- A simple GitHub Actions workflow that builds and runs this program inside an Ubuntu 20.04 container and then collects the core dump and executable as artifacts
