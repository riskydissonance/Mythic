# Changelog
All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](http://keepachangelog.com/en/1.0.0/)
and this project adheres to [Semantic Versioning](http://semver.org/spec/v2.0.0.html).

## 0.2.2 - 2023-09-07

### Changed

- Updated environment variables to have `nginx_use_ipv4` and `nginx_use_ipv6` configuration options

## 0.2.1 - 2023-07-20

### Changed

- Updated environment variables to support *_mem_limit to restrict the memory usage by the various containers.
This applies to all containers that also support setting their cpu limits. To restrict to 2GB, set "2gb", to restrict to 512MB, set "512mb"

## 0.2.0 - 2023-07-19

### Changed

- Removed the hard-coded mythic docker network subnet of 172.100.0.0/16. With this update you need to tear down all containers and rebuild so that the new networking applies.

## 0.1.26 - 2023-07-18

### Changed

- Updated the docker-compose creation process to not exit on failing to read in a newly created yaml file

## 0.1.25 - 2023-07-05

### Changed

- Added `services` command to list out container status, image build status, and dockercompose entry status for all folders in InstalledServices

## 0.1.24 - 2023-06-20

### Changed

- Adjusted installs to not error out if documentation folders fail to install

## 0.1.23 - 2023-06-20

### Changed

- Fixed a control flow bug that would restart all containers if building a new single container

## v0.1.21 - 2023-06-14

### Changed
- Updated the `./mythic-cli status` command to break out a distinction between services in docker compose that aren't running and those not in docker compose

## v0.1.20 - 2023-06-14

### Changed

- Pulled in a PR to make sure documentation-wrapper information is pulled in on install for services
- Updated the `./mythic-cli status` command to list out additional services installed but not present in docker-compose
- Updated the `./mythic-cli config service` command to list out just configurations needed for remote agent development
- Added new variable, `mythic_server_dynamic_ports_bind_localhost_only`, specifically to control if dynamic ports are bound to localhost or not, separate from mythic_server

## v0.1.19 - 2023-06-07

### Changed

- Updated docker-compose to bind the Dynamic ports for Mythic to localhost if `mythic_server_bind_localhost_only` is set to true

## v0.1.17 - 2023-06-02

### Changed

- Updated mythic_jupyter docker-compose entry to keep the `deploy` key and all sub keys 
- Updated health check for mythic_nginx to use curl instead of wget

## v0.1.15 - 2023-05-17

### Changed

- re-building mythic service containers will re-generate their docker-compose file entries first

### Added

- Added a command to remove containers

## 0.1.14 - 2023-05-10

### Changed

- Fixed an issue where installing another services after mythic_sync would uninstall mythic_sync

## 0.1.13 - 2023-05-10

### Changed

- Updated failed installs to return exit code 1 instead of just printing error and exiting

## 0.1.9 - 2023-04-25

### Changed

- Updated Mythic's env to take in configuration channels for the various webhook types and mirror it to containers

## 0.1.8 - 2023-04-20

### changed

- mythic_sync installation pointed to normal service installation instead of mythic_sync install

## 0.1.6 - 2023-04-19

### Added

- Added DEFAULT_OPERATION_WEBHOOK_URL and DEFAULT_OPERATION_WEBHOOK_CHANNEL values

## 0.1.3 - 2023-03-16

### Changed

- updated install service functionality to also start the service 

## 0.1.0 - 2023-03-03

### Changed

- Updated to use viper and cobra 

## 0.0.8 - 2022-11-7

### Changed

- If the `services` section of the docker-compose.yml file is already set, then the `mythic-cli` binary doesn't modify it. This allows people to make small modifications (such as adding IPv6 addresses) without being overridden. The only field that gets statically changed back each time the mythic-cli binary is run is the `networks.default_network.driver_opts` field since the yaml parser will break up the `com.docker.network.bridge.name` field into subkeys rather than leaving it as a single key.
