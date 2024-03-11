# Dependabot fails on NuGet updates with `Block argument of NuGetConfigCredentialHelpers::patch_nuget_config_for_action causes an exception A compatible .NET SDK was not found.`

## Minimal reproduction

- https://github.com/austindrenski/dependabot-nuget-failure-2/network/updates/798517643

```
  proxy | 2024/03/11 16:32:44 proxy starting, commit: cf8623577dad71c128f219df2b27df6de35b909d
  proxy | 2024/03/11 16:32:44 Listening (:1080)
updater | 2024-03-11T16:32:45.449873260 [798517643:main:WARN:src/devices/src/legacy/serial.rs:222] Detached the serial input due to peer close/error.
updater | time="2024-03-11T16:32:48Z" level=info msg="guest starting" commit=6ee2dfdd9de690457a831bc6c065b2ec4acdd0b7
updater | time="2024-03-11T16:32:48Z" level=info msg="starting job..." fetcher_timeout=10m0s job_id=798517643 updater_timeout=45m0s updater_version=987861db033956fd10eb8a353c8efae8e827d827-nuget
updater | 2024/03/11 16:32:58 INFO <job_798517643> Starting job processing
updater | 2024/03/11 16:32:58 INFO <job_798517643> Job definition: {"job":{"allowed-updates":[{"dependency-type":"direct","update-type":"all"}],"commit-message-options":{"include-scope":null,"prefix":null,"prefix-development":null},"credentials-metadata":[{"host":"github.com","type":"git_source"}],"debug":null,"dependencies":null,"dependency-group-to-refresh":null,"dependency-groups":[],"existing-group-pull-requests":[],"existing-pull-requests":[],"experiments":{"proxy-cached":true,"record-ecosystem-versions":true,"record-update-job-unknown-error":true},"ignore-conditions":[],"lockfile-only":false,"max-updater-run-time":2700,"package-manager":"nuget","proxy-log-response-body-on-auth-failure":true,"reject-external-code":false,"repo-private":false,"requirements-update-strategy":null,"security-advisories":[],"security-updates-only":false,"source":{"api-endpoint":"https://api.github.com/","branch":null,"directory":"/.","hostname":"github.com","provider":"github","repo":"austindrenski/dependabot-nuget-failure-2"},"update-subdependencies":false,"updating-a-pull-request":false,"vendor-dependencies":false}}
updater | 
  proxy | 2024/03/11 16:32:58 [002] GET https://github.com:443/austindrenski/dependabot-nuget-failure-2/info/refs?service=git-upload-pack
  proxy | 2024/03/11 16:32:58 [002] * authenticating git server request (host: github.com)
  proxy | 2024/03/11 16:32:59 [002] 200 https://github.com:443/austindrenski/dependabot-nuget-failure-2/info/refs?service=git-upload-pack
  proxy | 2024/03/11 16:32:59 [004] POST https://github.com:443/austindrenski/dependabot-nuget-failure-2/git-upload-pack
  proxy | 2024/03/11 16:32:59 [004] * authenticating git server request (host: github.com)
  proxy | 2024/03/11 16:32:59 [004] 200 https://github.com:443/austindrenski/dependabot-nuget-failure-2/git-upload-pack
  proxy | 2024/03/11 16:32:59 [006] POST https://github.com:443/austindrenski/dependabot-nuget-failure-2/git-upload-pack
  proxy | 2024/03/11 16:32:59 [006] * authenticating git server request (host: github.com)
  proxy | 2024/03/11 16:32:59 [006] 200 https://github.com:443/austindrenski/dependabot-nuget-failure-2/git-upload-pack
updater | 2024/03/11 16:32:59 INFO <job_798517643> Finished job processing
updater | time="2024-03-11T16:32:59Z" level=info msg="task complete" container_id=job-798517643-file-fetcher exit_code=0 job_id=798517643 step=fetcher
updater | 2024/03/11 16:33:05 INFO <job_798517643> Starting job processing
  proxy | 2024/03/11 16:33:05 [008] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/index.json
  proxy | 2024/03/11 16:33:05 [008] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/index.json
  proxy | 2024/03/11 16:33:06 [010] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.0.0-preview/3.3.5.json
  proxy | 2024/03/11 16:33:06 [010] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.0.0-preview/3.3.5.json
  proxy | 2024/03/11 16:33:06 [012] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.3.5.1/3.3.21.16.json
  proxy | 2024/03/11 16:33:06 [012] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.3.5.1/3.3.21.16.json
  proxy | 2024/03/11 16:33:06 [014] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.3.21.17/3.3.31.7.json
  proxy | 2024/03/11 16:33:06 [014] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.3.21.17/3.3.31.7.json
  proxy | 2024/03/11 16:33:07 [016] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.3.31.8/3.3.103.19.json
  proxy | 2024/03/11 16:33:07 [016] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.3.31.8/3.3.103.19.json
  proxy | 2024/03/11 16:33:07 [018] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.3.103.20/3.3.104.11.json
  proxy | 2024/03/11 16:33:07 [018] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.3.103.20/3.3.104.11.json
  proxy | 2024/03/11 16:33:07 [020] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.3.104.12/3.3.106.26.json
  proxy | 2024/03/11 16:33:07 [020] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.3.104.12/3.3.106.26.json
  proxy | 2024/03/11 16:33:07 [022] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.3.106.27/3.5.1.18.json
  proxy | 2024/03/11 16:33:07 [022] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.3.106.27/3.5.1.18.json
  proxy | 2024/03/11 16:33:08 [024] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.5.1.19/3.7.0.json
  proxy | 2024/03/11 16:33:08 [024] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.5.1.19/3.7.0.json
  proxy | 2024/03/11 16:33:08 [026] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.7.0.1/3.7.3.1.json
  proxy | 2024/03/11 16:33:08 [026] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.7.0.1/3.7.3.1.json
  proxy | 2024/03/11 16:33:08 [028] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.7.3.2/3.7.7.1.json
  proxy | 2024/03/11 16:33:08 [028] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.7.3.2/3.7.7.1.json
  proxy | 2024/03/11 16:33:08 [030] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.7.7.2/3.7.12.14.json
  proxy | 2024/03/11 16:33:08 [030] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.7.7.2/3.7.12.14.json
  proxy | 2024/03/11 16:33:08 [032] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.7.12.15/3.7.100.23.json
  proxy | 2024/03/11 16:33:08 [032] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.7.12.15/3.7.100.23.json
  proxy | 2024/03/11 16:33:09 [034] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.7.100.24/3.7.105.15.json
  proxy | 2024/03/11 16:33:09 [034] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.7.100.24/3.7.105.15.json
  proxy | 2024/03/11 16:33:09 [036] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.7.105.16/3.7.107.11.json
  proxy | 2024/03/11 16:33:09 [036] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.7.105.16/3.7.107.11.json
  proxy | 2024/03/11 16:33:09 [038] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.7.107.12/3.7.204.4.json
  proxy | 2024/03/11 16:33:09 [038] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.7.107.12/3.7.204.4.json
  proxy | 2024/03/11 16:33:09 [040] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.7.204.5/3.7.302.11.json
  proxy | 2024/03/11 16:33:09 [040] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.7.204.5/3.7.302.11.json
  proxy | 2024/03/11 16:33:09 [042] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.7.302.12/3.7.302.16.json
  proxy | 2024/03/11 16:33:09 [042] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.core/page/3.7.302.12/3.7.302.16.json
  proxy | 2024/03/11 16:33:09 [044] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/index.json
  proxy | 2024/03/11 16:33:09 [044] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/index.json
  proxy | 2024/03/11 16:33:09 [046] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.0.0-preview/3.3.4.16.json
  proxy | 2024/03/11 16:33:09 [046] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.0.0-preview/3.3.4.16.json
  proxy | 2024/03/11 16:33:10 [048] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.3.4.17/3.3.17.1.json
  proxy | 2024/03/11 16:33:10 [048] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.3.4.17/3.3.17.1.json
  proxy | 2024/03/11 16:33:10 [050] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.3.17.2/3.3.101.41.json
  proxy | 2024/03/11 16:33:10 [050] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.3.17.2/3.3.101.41.json
  proxy | 2024/03/11 16:33:10 [052] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.3.101.42/3.3.104.8.json
  proxy | 2024/03/11 16:33:10 [052] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.3.101.42/3.3.104.8.json
  proxy | 2024/03/11 16:33:10 [054] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.3.104.9/3.3.106.2.json
  proxy | 2024/03/11 16:33:10 [054] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.3.104.9/3.3.106.2.json
  proxy | 2024/03/11 16:33:10 [056] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.3.106.3/3.5.0.17.json
  proxy | 2024/03/11 16:33:10 [056] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.3.106.3/3.5.0.17.json
  proxy | 2024/03/11 16:33:10 [058] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.5.0.18/3.5.4.38.json
  proxy | 2024/03/11 16:33:10 [058] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.5.0.18/3.5.4.38.json
  proxy | 2024/03/11 16:33:10 [060] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.7.0/3.7.0.63.json
  proxy | 2024/03/11 16:33:10 [060] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.7.0/3.7.0.63.json
  proxy | 2024/03/11 16:33:10 [062] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.7.0.64/3.7.2.20.json
  proxy | 2024/03/11 16:33:10 [062] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.7.0.64/3.7.2.20.json
  proxy | 2024/03/11 16:33:11 [064] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.7.3/3.7.3.63.json
  proxy | 2024/03/11 16:33:11 [064] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.7.3/3.7.3.63.json
  proxy | 2024/03/11 16:33:11 [066] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.7.3.64/3.7.100.23.json
  proxy | 2024/03/11 16:33:11 [066] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.7.3.64/3.7.100.23.json
  proxy | 2024/03/11 16:33:11 [068] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.7.100.24/3.7.102.json
  proxy | 2024/03/11 16:33:11 [068] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.7.100.24/3.7.102.json
  proxy | 2024/03/11 16:33:11 [070] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.7.102.1/3.7.104.json
  proxy | 2024/03/11 16:33:11 [070] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.7.102.1/3.7.104.json
  proxy | 2024/03/11 16:33:11 [072] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.7.104.1/3.7.202.7.json
  proxy | 2024/03/11 16:33:11 [072] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.7.104.1/3.7.202.7.json
  proxy | 2024/03/11 16:33:11 [074] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.7.203/3.7.301.7.json
  proxy | 2024/03/11 16:33:11 [074] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.7.203/3.7.301.7.json
  proxy | 2024/03/11 16:33:11 [076] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.7.301.8/3.7.301.19.json
  proxy | 2024/03/11 16:33:12 [076] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.dynamodbv2/page/3.7.301.8/3.7.301.19.json
  proxy | 2024/03/11 16:33:12 [078] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/index.json
  proxy | 2024/03/11 16:33:12 [078] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/index.json
  proxy | 2024/03/11 16:33:12 [080] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.0.0-preview/3.3.5.2.json
  proxy | 2024/03/11 16:33:12 [080] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.0.0-preview/3.3.5.2.json
  proxy | 2024/03/11 16:33:12 [082] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.3.5.3/3.3.23.json
  proxy | 2024/03/11 16:33:12 [082] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.3.5.3/3.3.23.json
  proxy | 2024/03/11 16:33:12 [084] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.3.23.1/3.3.101.7.json
  proxy | 2024/03/11 16:33:12 [084] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.3.23.1/3.3.101.7.json
  proxy | 2024/03/11 16:33:12 [086] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.3.101.8/3.3.104.23.json
  proxy | 2024/03/11 16:33:12 [086] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.3.101.8/3.3.104.23.json
  proxy | 2024/03/11 16:33:12 [088] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.3.104.24/3.3.110.20.json
  proxy | 2024/03/11 16:33:12 [088] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.3.104.24/3.3.110.20.json
  proxy | 2024/03/11 16:33:13 [090] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.3.110.21/3.3.111.11.json
  proxy | 2024/03/11 16:33:13 [090] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.3.110.21/3.3.111.11.json
  proxy | 2024/03/11 16:33:13 [092] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.3.111.12/3.5.3.4.json
  proxy | 2024/03/11 16:33:13 [092] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.3.111.12/3.5.3.4.json
  proxy | 2024/03/11 16:33:13 [094] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.5.3.5/3.7.0.4.json
  proxy | 2024/03/11 16:33:13 [094] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.5.3.5/3.7.0.4.json
  proxy | 2024/03/11 16:33:13 [096] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.7.0.5/3.7.2.3.json
  proxy | 2024/03/11 16:33:13 [096] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.7.0.5/3.7.2.3.json
  proxy | 2024/03/11 16:33:13 [098] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.7.2.4/3.7.7.21.json
  proxy | 2024/03/11 16:33:13 [098] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.7.2.4/3.7.7.21.json
  proxy | 2024/03/11 16:33:13 [100] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.7.7.22/3.7.9.29.json
  proxy | 2024/03/11 16:33:13 [100] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.7.7.22/3.7.9.29.json
  proxy | 2024/03/11 16:33:13 [102] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.7.9.30/3.7.101.18.json
  proxy | 2024/03/11 16:33:13 [102] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.7.9.30/3.7.101.18.json
  proxy | 2024/03/11 16:33:13 [104] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.7.101.19/3.7.103.17.json
  proxy | 2024/03/11 16:33:13 [104] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.7.101.19/3.7.103.17.json
  proxy | 2024/03/11 16:33:14 [106] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.7.103.18/3.7.104.29.json
  proxy | 2024/03/11 16:33:14 [106] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.7.103.18/3.7.104.29.json
  proxy | 2024/03/11 16:33:14 [108] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.7.104.30/3.7.205.2.json
  proxy | 2024/03/11 16:33:14 [108] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.7.104.30/3.7.205.2.json
  proxy | 2024/03/11 16:33:14 [110] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.7.205.3/3.7.305.15.json
  proxy | 2024/03/11 16:33:14 [110] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.7.205.3/3.7.305.15.json
  proxy | 2024/03/11 16:33:14 [112] GET https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.7.305.16/3.7.305.31.json
  proxy | 2024/03/11 16:33:14 [112] 200 https://api.nuget.org:443/v3/registration5-gz-semver2/awssdk.s3/page/3.7.305.16/3.7.305.31.json
  proxy | 2024/03/11 16:33:14 [114] GET https://api.nuget.org:443/v3-flatcontainer/awssdk.core/3.7.302.15/awssdk.core.nuspec
  proxy | 2024/03/11 16:33:14 [114] 200 https://api.nuget.org:443/v3-flatcontainer/awssdk.core/3.7.302.15/awssdk.core.nuspec
  proxy | 2024/03/11 16:33:14 [116] GET https://api.nuget.org:443/v3-flatcontainer/microsoft.bcl.asyncinterfaces/1.1.0/microsoft.bcl.asyncinterfaces.nuspec
  proxy | 2024/03/11 16:33:14 [116] 200 https://api.nuget.org:443/v3-flatcontainer/microsoft.bcl.asyncinterfaces/1.1.0/microsoft.bcl.asyncinterfaces.nuspec
  proxy | 2024/03/11 16:33:14 [118] GET https://api.nuget.org:443/v3-flatcontainer/system.threading.tasks.extensions/4.5.2/system.threading.tasks.extensions.nuspec
  proxy | 2024/03/11 16:33:14 [118] 200 https://api.nuget.org:443/v3-flatcontainer/system.threading.tasks.extensions/4.5.2/system.threading.tasks.extensions.nuspec
  proxy | 2024/03/11 16:33:14 [120] GET https://api.nuget.org:443/v3-flatcontainer/system.runtime.compilerservices.unsafe/4.5.2/system.runtime.compilerservices.unsafe.nuspec
  proxy | 2024/03/11 16:33:14 [120] 200 https://api.nuget.org:443/v3-flatcontainer/system.runtime.compilerservices.unsafe/4.5.2/system.runtime.compilerservices.unsafe.nuspec
  proxy | 2024/03/11 16:33:14 [122] GET https://api.nuget.org:443/v3-flatcontainer/system.runtime/4.3.0/system.runtime.nuspec
  proxy | 2024/03/11 16:33:14 [122] 200 https://api.nuget.org:443/v3-flatcontainer/system.runtime/4.3.0/system.runtime.nuspec
  proxy | 2024/03/11 16:33:14 [124] GET https://api.nuget.org:443/v3-flatcontainer/microsoft.netcore.platforms/1.1.0/microsoft.netcore.platforms.nuspec
  proxy | 2024/03/11 16:33:14 [124] 200 https://api.nuget.org:443/v3-flatcontainer/microsoft.netcore.platforms/1.1.0/microsoft.netcore.platforms.nuspec
  proxy | 2024/03/11 16:33:14 [126] GET https://api.nuget.org:443/v3-flatcontainer/microsoft.netcore.targets/1.1.0/microsoft.netcore.targets.nuspec
  proxy | 2024/03/11 16:33:14 [126] 200 https://api.nuget.org:443/v3-flatcontainer/microsoft.netcore.targets/1.1.0/microsoft.netcore.targets.nuspec
  proxy | 2024/03/11 16:33:15 [128] GET https://api.nuget.org:443/v3-flatcontainer/system.collections/4.3.0/system.collections.nuspec
  proxy | 2024/03/11 16:33:15 [128] 200 https://api.nuget.org:443/v3-flatcontainer/system.collections/4.3.0/system.collections.nuspec
  proxy | 2024/03/11 16:33:15 [130] GET https://api.nuget.org:443/v3-flatcontainer/system.threading.tasks/4.3.0/system.threading.tasks.nuspec
  proxy | 2024/03/11 16:33:15 [130] 200 https://api.nuget.org:443/v3-flatcontainer/system.threading.tasks/4.3.0/system.threading.tasks.nuspec
  proxy | 2024/03/11 16:33:15 [132] GET https://api.nuget.org:443/v3-flatcontainer/awssdk.dynamodbv2/3.7.301.18/awssdk.dynamodbv2.nuspec
  proxy | 2024/03/11 16:33:15 [132] 200 https://api.nuget.org:443/v3-flatcontainer/awssdk.dynamodbv2/3.7.301.18/awssdk.dynamodbv2.nuspec
  proxy | 2024/03/11 16:33:15 [134] GET https://api.nuget.org:443/v3-flatcontainer/awssdk.s3/3.7.305.30/awssdk.s3.nuspec
  proxy | 2024/03/11 16:33:15 [134] 200 https://api.nuget.org:443/v3-flatcontainer/awssdk.s3/3.7.305.30/awssdk.s3.nuspec
updater | 2024/03/11 16:33:16 INFO <job_798517643> Starting update job for austindrenski/dependabot-nuget-failure-2
updater | 2024/03/11 16:33:16 INFO <job_798517643> Checking all dependencies for version updates...
updater | 2024/03/11 16:33:16 INFO <job_798517643> Checking if AWSSDK.Core 3.7.302.15 needs updating
  proxy | 2024/03/11 16:33:17 [142] GET https://api.nuget.org:443/v3-flatcontainer/awssdk.core/3.7.302.15/awssdk.core.nuspec
  proxy | 2024/03/11 16:33:17 [142] 200 https://api.nuget.org:443/v3-flatcontainer/awssdk.core/3.7.302.15/awssdk.core.nuspec
updater | running NuGet updater:
updater | /opt/nuget/NuGetUpdater/NuGetUpdater.Cli framework-check --project-tfms net8.0 --package-tfms .NETFramework3.5 .NETFramework4.5 .NETStandard2.0 .NETCoreApp3.1 .NETCoreApp8.0 --verbose
updater | The package is compatible.
  proxy | 2024/03/11 16:33:18 [144] GET https://api.nuget.org:443/v3-flatcontainer/awssdk.core/3.7.302.16/awssdk.core.nuspec
  proxy | 2024/03/11 16:33:18 [144] 200 https://api.nuget.org:443/v3-flatcontainer/awssdk.core/3.7.302.16/awssdk.core.nuspec
updater | 2024/03/11 16:33:18 INFO <job_798517643> Latest version is 3.7.302.16
updater | 2024/03/11 16:33:18 INFO <job_798517643> Requirements to unlock all
updater | 2024/03/11 16:33:18 INFO <job_798517643> Requirements update strategy 
updater | Finding updated dependencies for AWSSDK.Core.
  proxy | 2024/03/11 16:33:18 [146] GET https://api.nuget.org:443/v3-flatcontainer/awssdk.core/3.7.302.16/awssdk.core.nuspec
  proxy | 2024/03/11 16:33:18 [146] 200 https://api.nuget.org:443/v3-flatcontainer/awssdk.core/3.7.302.16/awssdk.core.nuspec
updater | 2024/03/11 16:33:18 INFO <job_798517643> Updating AWSSDK.Core from 3.7.302.15 to 3.7.302.16
updater | running NuGet updater:
updater | /opt/nuget/NuGetUpdater/NuGetUpdater.Cli update --repo-root /home/dependabot/dependabot-updater/repo --solution-or-project /home/dependabot/dependabot-updater/repo/src/SomeProject/SomeProject.csproj --dependency AWSSDK.Core --new-version 3.7.302.16 --previous-version 3.7.302.15 --verbose
updater | 2024/03/11 16:33:19 ERROR <job_798517643> Block argument of NuGetConfigCredentialHelpers::patch_nuget_config_for_action causes an exception A compatible .NET SDK was not found.
updater | 
updater | Requested SDK version: 8.0.201
updater | global.json file: /home/dependabot/dependabot-updater/repo/global.json
updater | 
updater | Installed SDKs:
updater | 
updater | Install the [8.0.201] .NET SDK or update [/home/dependabot/dependabot-updater/repo/global.json] to match an installed SDK.
updater | 
updater | Learn about SDK resolution:
updater | https://aka.ms/dotnet/sdk-not-found
updater | Unhandled exception: System.TypeInitializationException: The type initializer for 'NuGetUpdater.Core.MSBuildHelper' threw an exception.
updater |  ---> System.InvalidOperationException: Failed to find all versions of .NET Core MSBuild. Call to hostfxr_resolve_sdk2. There may be more details in stderr.
updater |    at Microsoft.Build.Locator.DotNetSdkLocationHelper.GetSdkFromGlobalSettings(String workingDirectory)
updater |    at Microsoft.Build.Locator.DotNetSdkLocationHelper.GetDotNetBasePaths(String workingDirectory)+MoveNext()
updater |    at Microsoft.Build.Locator.DotNetSdkLocationHelper.GetInstances(String workingDirectory)+MoveNext()
updater |    at Microsoft.Build.Locator.MSBuildLocator.GetInstances(VisualStudioInstanceQueryOptions options)+MoveNext()
updater |    at System.Linq.Enumerable.WhereEnumerableIterator`1.MoveNext()
updater |    at System.Linq.Enumerable.TryGetFirst[TSource](IEnumerable`1 source, Boolean& found)
updater |    at System.Linq.Enumerable.First[TSource](IEnumerable`1 source)
updater |    at NuGetUpdater.Core.MSBuildHelper.RegisterMSBuild() in /opt/nuget/lib/NuGetUpdater/NuGetUpdater.Core/Utilities/MSBuildHelper.cs:line 42
updater |    at NuGetUpdater.Core.MSBuildHelper..cctor() in /opt/nuget/lib/NuGetUpdater/NuGetUpdater.Core/Utilities/MSBuildHelper.cs:line 34
updater |    --- End of inner exception stack trace ---
updater |    at NuGetUpdater.Core.MSBuildHelper.RegisterMSBuild() in /opt/nuget/lib/NuGetUpdater/NuGetUpdater.Core/Utilities/MSBuildHelper.cs:line 40
updater |    at NuGetUpdater.Core.UpdaterWorker.RunAsync(String repoRootPath, String workspacePath, String dependencyName, String previousDependencyVersion, String newDependencyVersion, Boolean isTransitive) in /opt/nuget/lib/NuGetUpdater/NuGetUpdater.Core/Updater/UpdaterWorker.cs:line 22
updater |    at NuGetUpdater.Cli.Commands.UpdateCommand.<>c__DisplayClass7_0.<<GetCommand>b__0>d.MoveNext() in /opt/nuget/lib/NuGetUpdater/NuGetUpdater.Cli/Commands/UpdateCommand.cs:line 37
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Invocation.AnonymousCommandHandler.InvokeAsync(InvocationContext context)
updater |    at System.CommandLine.Invocation.InvocationPipeline.<>c__DisplayClass4_0.<<BuildInvocationChain>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass17_0.<<UseParseErrorReporting>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass12_0.<<UseHelp>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass22_0.<<UseVersionOption>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass19_0.<<UseTypoCorrections>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c.<<UseSuggestDirective>b__18_0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass16_0.<<UseParseDirective>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c.<<RegisterWithDotnetSuggest>b__5_0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass8_0.<<UseExceptionHandler>b__0>d.MoveNext()
updater | 8.0.100 [/usr/local/dotnet/current/sdk]:
updater | A compatible .NET SDK was not found.
updater | 
updater | Requested SDK version: 8.0.201
updater | global.json file: /home/dependabot/dependabot-updater/repo/global.json
updater | 
updater | Installed SDKs:
updater | 
updater | Install the [8.0.201] .NET SDK or update [/home/dependabot/dependabot-updater/repo/global.json] to match an installed SDK.
updater | 
updater | Learn about SDK resolution:
updater | https://aka.ms/dotnet/sdk-not-found
updater | Unhandled exception: System.TypeInitializationException: The type initializer for 'NuGetUpdater.Core.MSBuildHelper' threw an exception.
updater |  ---> System.InvalidOperationException: Failed to find all versions of .NET Core MSBuild. Call to hostfxr_resolve_sdk2. There may be more details in stderr.
updater |    at Microsoft.Build.Locator.DotNetSdkLocationHelper.GetSdkFromGlobalSettings(String workingDirectory)
updater |    at Microsoft.Build.Locator.DotNetSdkLocationHelper.GetDotNetBasePaths(String workingDirectory)+MoveNext()
updater |    at Microsoft.Build.Locator.DotNetSdkLocationHelper.GetInstances(String workingDirectory)+MoveNext()
updater |    at Microsoft.Build.Locator.MSBuildLocator.GetInstances(VisualStudioInstanceQueryOptions options)+MoveNext()
updater |    at System.Linq.Enumerable.WhereEnumerableIterator`1.MoveNext()
updater |    at System.Linq.Enumerable.TryGetFirst[TSource](IEnumerable`1 source, Boolean& found)
updater |    at System.Linq.Enumerable.First[TSource](IEnumerable`1 source)
updater |    at NuGetUpdater.Core.MSBuildHelper.RegisterMSBuild() in /opt/nuget/lib/NuGetUpdater/NuGetUpdater.Core/Utilities/MSBuildHelper.cs:line 42
updater |    at NuGetUpdater.Core.MSBuildHelper..cctor() in /opt/nuget/lib/NuGetUpdater/NuGetUpdater.Core/Utilities/MSBuildHelper.cs:line 34
updater |    --- End of inner exception stack trace ---
updater |    at NuGetUpdater.Core.MSBuildHelper.RegisterMSBuild() in /opt/nuget/lib/NuGetUpdater/NuGetUpdater.Core/Utilities/MSBuildHelper.cs:line 40
updater |    at NuGetUpdater.Core.UpdaterWorker.RunAsync(String repoRootPath, String workspacePath, String dependencyName, String previousDependencyVersion, String newDependencyVersion, Boolean isTransitive) in /opt/nuget/lib/NuGetUpdater/NuGetUpdater.Core/Updater/UpdaterWorker.cs:line 22
updater |    at NuGetUpdater.Cli.Commands.UpdateCommand.<>c__DisplayClass7_0.<<GetCommand>b__0>d.MoveNext() in /opt/nuget/lib/NuGetUpdater/NuGetUpdater.Cli/Commands/UpdateCommand.cs:line 37
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Invocation.AnonymousCommandHandler.InvokeAsync(InvocationContext context)
updater |    at System.CommandLine.Invocation.InvocationPipeline.<>c__DisplayClass4_0.<<BuildInvocationChain>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass17_0.<<UseParseErrorReporting>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass12_0.<<UseHelp>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass22_0.<<UseVersionOption>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass19_0.<<UseTypoCorrections>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c.<<UseSuggestDirective>b__18_0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass16_0.<<UseParseDirective>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c.<<RegisterWithDotnetSuggest>b__5_0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass8_0.<<UseExceptionHandler>b__0>d.MoveNext()
updater | 8.0.100 [/usr/local/dotnet/current/sdk]
updater | 
updater | 2024/03/11 16:33:20 ERROR <job_798517643> Error processing AWSSDK.Core (Dependabot::DependabotError)
updater | 2024/03/11 16:33:20 ERROR <job_798517643> FileUpdater failed
updater | 2024/03/11 16:33:20 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/dependency_change_builder.rb:69:in `run'
updater | 2024/03/11 16:33:20 ERROR <job_798517643> /home/dependabot/dependabot-updater/vendor/ruby/3.1.0/gems/sorbet-runtime-0.5.11193/lib/types/private/methods/call_validation.rb:272:in `bind_call'
updater | 2024/03/11 16:33:20 ERROR <job_798517643> /home/dependabot/dependabot-updater/vendor/ruby/3.1.0/gems/sorbet-runtime-0.5.11193/lib/types/private/methods/call_validation.rb:272:in `validate_call'
updater | 2024/03/11 16:33:20 ERROR <job_798517643> /home/dependabot/dependabot-updater/vendor/ruby/3.1.0/gems/sorbet-runtime-0.5.11193/lib/types/private/methods/_methods.rb:272:in `block in _on_method_added'
updater | 2024/03/11 16:33:20 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/dependency_change_builder.rb:42:in `create_from'
updater | 2024/03/11 16:33:20 ERROR <job_798517643> /home/dependabot/dependabot-updater/vendor/ruby/3.1.0/gems/sorbet-runtime-0.5.11193/lib/types/private/methods/call_validation.rb:272:in `bind_call'
updater | 2024/03/11 16:33:20 ERROR <job_798517643> /home/dependabot/dependabot-updater/vendor/ruby/3.1.0/gems/sorbet-runtime-0.5.11193/lib/types/private/methods/call_validation.rb:272:in `validate_call'
updater | 2024/03/11 16:33:20 ERROR <job_798517643> /home/dependabot/dependabot-updater/vendor/ruby/3.1.0/gems/sorbet-runtime-0.5.11193/lib/types/private/methods/_methods.rb:272:in `block in _on_method_added'
updater | 2024/03/11 16:33:20 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/updater/operations/update_all_versions.rb:132:in `check_and_create_pull_request'
updater | 2024/03/11 16:33:20 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/updater/operations/update_all_versions.rb:64:in `check_and_create_pr_with_error_handling'
updater | 2024/03/11 16:33:20 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/updater/operations/update_all_versions.rb:39:in `block in perform'
updater | 2024/03/11 16:33:20 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/updater/operations/update_all_versions.rb:39:in `each'
updater | 2024/03/11 16:33:20 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/updater/operations/update_all_versions.rb:39:in `perform'
updater | 2024/03/11 16:33:20 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/updater.rb:45:in `run'
updater | 2024/03/11 16:33:20 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/update_files_command.rb:43:in `block in perform_job'
updater | 2024/03/11 16:33:20 ERROR <job_798517643> /home/dependabot/dependabot-updater/vendor/ruby/3.1.0/gems/opentelemetry-api-1.2.3/lib/opentelemetry/trace/tracer.rb:37:in `block in in_span'
updater | 2024/03/11 16:33:20 ERROR <job_798517643> /home/dependabot/dependabot-updater/vendor/ruby/3.1.0/gems/opentelemetry-api-1.2.3/lib/opentelemetry/trace.rb:70:in `block in with_span'
updater | 2024/03/11 16:33:20 ERROR <job_798517643> /home/dependabot/dependabot-updater/vendor/ruby/3.1.0/gems/opentelemetry-api-1.2.3/lib/opentelemetry/context.rb:87:in `with_value'
updater | 2024/03/11 16:33:20 ERROR <job_798517643> /home/dependabot/dependabot-updater/vendor/ruby/3.1.0/gems/opentelemetry-api-1.2.3/lib/opentelemetry/trace.rb:70:in `with_span'
updater | 2024/03/11 16:33:20 ERROR <job_798517643> /home/dependabot/dependabot-updater/vendor/ruby/3.1.0/gems/opentelemetry-api-1.2.3/lib/opentelemetry/trace/tracer.rb:37:in `in_span'
updater | 2024/03/11 16:33:20 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/update_files_command.rb:17:in `perform_job'
updater | 2024/03/11 16:33:20 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/base_command.rb:36:in `run'
updater | 2024/03/11 16:33:20 ERROR <job_798517643> bin/update_files.rb:24:in `<main>'
updater | 2024/03/11 16:33:20 INFO <job_798517643> Checking if AWSSDK.S3 3.7.305.30 needs updating
  proxy | 2024/03/11 16:33:20 [160] GET https://api.nuget.org:443/v3-flatcontainer/awssdk.s3/3.7.305.30/awssdk.s3.nuspec
  proxy | 2024/03/11 16:33:20 [160] 200 https://api.nuget.org:443/v3-flatcontainer/awssdk.s3/3.7.305.30/awssdk.s3.nuspec
  proxy | 2024/03/11 16:33:20 [162] GET https://api.nuget.org:443/v3-flatcontainer/awssdk.s3/3.7.305.30/awssdk.s3.3.7.305.30.nupkg
  proxy | 2024/03/11 16:33:20 [162] 200 https://api.nuget.org:443/v3-flatcontainer/awssdk.s3/3.7.305.30/awssdk.s3.3.7.305.30.nupkg
updater | running NuGet updater:
updater | /opt/nuget/NuGetUpdater/NuGetUpdater.Cli framework-check --project-tfms net8.0 --package-tfms net35 net45 netstandard2.0 netcoreapp3.1 net8.0 --verbose
updater | The package is compatible.
  proxy | 2024/03/11 16:33:22 [164] GET https://api.nuget.org:443/v3-flatcontainer/awssdk.s3/3.7.305.31/awssdk.s3.nuspec
  proxy | 2024/03/11 16:33:22 [164] 200 https://api.nuget.org:443/v3-flatcontainer/awssdk.s3/3.7.305.31/awssdk.s3.nuspec
  proxy | 2024/03/11 16:33:22 [166] GET https://api.nuget.org:443/v3-flatcontainer/awssdk.s3/3.7.305.31/awssdk.s3.3.7.305.31.nupkg
  proxy | 2024/03/11 16:33:22 [166] 200 https://api.nuget.org:443/v3-flatcontainer/awssdk.s3/3.7.305.31/awssdk.s3.3.7.305.31.nupkg
updater | 2024/03/11 16:33:22 INFO <job_798517643> Latest version is 3.7.305.31
updater | 2024/03/11 16:33:22 INFO <job_798517643> Requirements to unlock all
updater | 2024/03/11 16:33:22 INFO <job_798517643> Requirements update strategy 
updater | Finding updated dependencies for AWSSDK.S3.
  proxy | 2024/03/11 16:33:22 [168] GET https://api.nuget.org:443/v3-flatcontainer/awssdk.s3/3.7.305.31/awssdk.s3.nuspec
  proxy | 2024/03/11 16:33:22 [168] 200 https://api.nuget.org:443/v3-flatcontainer/awssdk.s3/3.7.305.31/awssdk.s3.nuspec
updater | 2024/03/11 16:33:22 INFO <job_798517643> Updating AWSSDK.S3 from 3.7.305.30 to 3.7.305.31
updater | running NuGet updater:
updater | /opt/nuget/NuGetUpdater/NuGetUpdater.Cli update --repo-root /home/dependabot/dependabot-updater/repo --solution-or-project /home/dependabot/dependabot-updater/repo/src/SomeProject/SomeProject.csproj --dependency AWSSDK.S3 --new-version 3.7.305.31 --previous-version 3.7.305.30 --verbose
updater | 2024/03/11 16:33:22 ERROR <job_798517643> Block argument of NuGetConfigCredentialHelpers::patch_nuget_config_for_action causes an exception A compatible .NET SDK was not found.
updater | 
updater | Requested SDK version: 8.0.201
updater | global.json file: /home/dependabot/dependabot-updater/repo/global.json
updater | 
updater | Installed SDKs:
updater | 
updater | Install the [8.0.201] .NET SDK or update [/home/dependabot/dependabot-updater/repo/global.json] to match an installed SDK.
updater | 
updater | Learn about SDK resolution:
updater | https://aka.ms/dotnet/sdk-not-found
updater | Unhandled exception: System.TypeInitializationException: The type initializer for 'NuGetUpdater.Core.MSBuildHelper' threw an exception.
updater |  ---> System.InvalidOperationException: Failed to find all versions of .NET Core MSBuild. Call to hostfxr_resolve_sdk2. There may be more details in stderr.
updater |    at Microsoft.Build.Locator.DotNetSdkLocationHelper.GetSdkFromGlobalSettings(String workingDirectory)
updater |    at Microsoft.Build.Locator.DotNetSdkLocationHelper.GetDotNetBasePaths(String workingDirectory)+MoveNext()
updater |    at Microsoft.Build.Locator.DotNetSdkLocationHelper.GetInstances(String workingDirectory)+MoveNext()
updater |    at Microsoft.Build.Locator.MSBuildLocator.GetInstances(VisualStudioInstanceQueryOptions options)+MoveNext()
updater |    at System.Linq.Enumerable.WhereEnumerableIterator`1.MoveNext()
updater |    at System.Linq.Enumerable.TryGetFirst[TSource](IEnumerable`1 source, Boolean& found)
updater |    at System.Linq.Enumerable.First[TSource](IEnumerable`1 source)
updater |    at NuGetUpdater.Core.MSBuildHelper.RegisterMSBuild() in /opt/nuget/lib/NuGetUpdater/NuGetUpdater.Core/Utilities/MSBuildHelper.cs:line 42
updater |    at NuGetUpdater.Core.MSBuildHelper..cctor() in /opt/nuget/lib/NuGetUpdater/NuGetUpdater.Core/Utilities/MSBuildHelper.cs:line 34
updater |    --- End of inner exception stack trace ---
updater |    at NuGetUpdater.Core.MSBuildHelper.RegisterMSBuild() in /opt/nuget/lib/NuGetUpdater/NuGetUpdater.Core/Utilities/MSBuildHelper.cs:line 40
updater |    at NuGetUpdater.Core.UpdaterWorker.RunAsync(String repoRootPath, String workspacePath, String dependencyName, String previousDependencyVersion, String newDependencyVersion, Boolean isTransitive) in /opt/nuget/lib/NuGetUpdater/NuGetUpdater.Core/Updater/UpdaterWorker.cs:line 22
updater |    at NuGetUpdater.Cli.Commands.UpdateCommand.<>c__DisplayClass7_0.<<GetCommand>b__0>d.MoveNext() in /opt/nuget/lib/NuGetUpdater/NuGetUpdater.Cli/Commands/UpdateCommand.cs:line 37
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Invocation.AnonymousCommandHandler.InvokeAsync(InvocationContext context)
updater |    at System.CommandLine.Invocation.InvocationPipeline.<>c__DisplayClass4_0.<<BuildInvocationChain>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass17_0.<<UseParseErrorReporting>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass12_0.<<UseHelp>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass22_0.<<UseVersionOption>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass19_0.<<UseTypoCorrections>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c.<<UseSuggestDirective>b__18_0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass16_0.<<UseParseDirective>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c.<<RegisterWithDotnetSuggest>b__5_0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass8_0.<<UseExceptionHandler>b__0>d.MoveNext()
updater | 8.0.100 [/usr/local/dotnet/current/sdk]:
updater | A compatible .NET SDK was not found.
updater | 
updater | Requested SDK version: 8.0.201
updater | global.json file: /home/dependabot/dependabot-updater/repo/global.json
updater | 
updater | Installed SDKs:
updater | 
updater | Install the [8.0.201] .NET SDK or update [/home/dependabot/dependabot-updater/repo/global.json] to match an installed SDK.
updater | 
updater | Learn about SDK resolution:
updater | https://aka.ms/dotnet/sdk-not-found
updater | Unhandled exception: System.TypeInitializationException: The type initializer for 'NuGetUpdater.Core.MSBuildHelper' threw an exception.
updater |  ---> System.InvalidOperationException: Failed to find all versions of .NET Core MSBuild. Call to hostfxr_resolve_sdk2. There may be more details in stderr.
updater |    at Microsoft.Build.Locator.DotNetSdkLocationHelper.GetSdkFromGlobalSettings(String workingDirectory)
updater |    at Microsoft.Build.Locator.DotNetSdkLocationHelper.GetDotNetBasePaths(String workingDirectory)+MoveNext()
updater |    at Microsoft.Build.Locator.DotNetSdkLocationHelper.GetInstances(String workingDirectory)+MoveNext()
updater |    at Microsoft.Build.Locator.MSBuildLocator.GetInstances(VisualStudioInstanceQueryOptions options)+MoveNext()
updater |    at System.Linq.Enumerable.WhereEnumerableIterator`1.MoveNext()
updater |    at System.Linq.Enumerable.TryGetFirst[TSource](IEnumerable`1 source, Boolean& found)
updater |    at System.Linq.Enumerable.First[TSource](IEnumerable`1 source)
updater |    at NuGetUpdater.Core.MSBuildHelper.RegisterMSBuild() in /opt/nuget/lib/NuGetUpdater/NuGetUpdater.Core/Utilities/MSBuildHelper.cs:line 42
updater |    at NuGetUpdater.Core.MSBuildHelper..cctor() in /opt/nuget/lib/NuGetUpdater/NuGetUpdater.Core/Utilities/MSBuildHelper.cs:line 34
updater |    --- End of inner exception stack trace ---
updater |    at NuGetUpdater.Core.MSBuildHelper.RegisterMSBuild() in /opt/nuget/lib/NuGetUpdater/NuGetUpdater.Core/Utilities/MSBuildHelper.cs:line 40
updater |    at NuGetUpdater.Core.UpdaterWorker.RunAsync(String repoRootPath, String workspacePath, String dependencyName, String previousDependencyVersion, String newDependencyVersion, Boolean isTransitive) in /opt/nuget/lib/NuGetUpdater/NuGetUpdater.Core/Updater/UpdaterWorker.cs:line 22
updater |    at NuGetUpdater.Cli.Commands.UpdateCommand.<>c__DisplayClass7_0.<<GetCommand>b__0>d.MoveNext() in /opt/nuget/lib/NuGetUpdater/NuGetUpdater.Cli/Commands/UpdateCommand.cs:line 37
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Invocation.AnonymousCommandHandler.InvokeAsync(InvocationContext context)
updater |    at System.CommandLine.Invocation.InvocationPipeline.<>c__DisplayClass4_0.<<BuildInvocationChain>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass17_0.<<UseParseErrorReporting>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass12_0.<<UseHelp>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass22_0.<<UseVersionOption>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass19_0.<<UseTypoCorrections>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c.<<UseSuggestDirective>b__18_0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass16_0.<<UseParseDirective>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c.<<RegisterWithDotnetSuggest>b__5_0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass8_0.<<UseExceptionHandler>b__0>d.MoveNext()
updater | 8.0.100 [/usr/local/dotnet/current/sdk]
updater | 
updater | 2024/03/11 16:33:23 ERROR <job_798517643> Error processing AWSSDK.S3 (Dependabot::DependabotError)
updater | 2024/03/11 16:33:23 ERROR <job_798517643> FileUpdater failed
updater | 2024/03/11 16:33:23 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/dependency_change_builder.rb:69:in `run'
updater | 2024/03/11 16:33:23 ERROR <job_798517643> /home/dependabot/dependabot-updater/vendor/ruby/3.1.0/gems/sorbet-runtime-0.5.11193/lib/types/private/methods/call_validation_2_7.rb:59:in `bind_call'
updater | 2024/03/11 16:33:23 ERROR <job_798517643> /home/dependabot/dependabot-updater/vendor/ruby/3.1.0/gems/sorbet-runtime-0.5.11193/lib/types/private/methods/call_validation_2_7.rb:59:in `block in create_validator_method_fast0'
updater | 2024/03/11 16:33:23 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/dependency_change_builder.rb:42:in `create_from'
updater | 2024/03/11 16:33:23 ERROR <job_798517643> /home/dependabot/dependabot-updater/vendor/ruby/3.1.0/gems/sorbet-runtime-0.5.11193/lib/types/private/methods/call_validation.rb:169:in `bind_call'
updater | 2024/03/11 16:33:23 ERROR <job_798517643> /home/dependabot/dependabot-updater/vendor/ruby/3.1.0/gems/sorbet-runtime-0.5.11193/lib/types/private/methods/call_validation.rb:169:in `validate_call_skip_block_type'
updater | 2024/03/11 16:33:23 ERROR <job_798517643> /home/dependabot/dependabot-updater/vendor/ruby/3.1.0/gems/sorbet-runtime-0.5.11193/lib/types/private/methods/call_validation.rb:111:in `block in create_validator_slow_skip_block_type'
updater | 2024/03/11 16:33:23 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/updater/operations/update_all_versions.rb:132:in `check_and_create_pull_request'
updater | 2024/03/11 16:33:23 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/updater/operations/update_all_versions.rb:64:in `check_and_create_pr_with_error_handling'
updater | 2024/03/11 16:33:23 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/updater/operations/update_all_versions.rb:39:in `block in perform'
updater | 2024/03/11 16:33:23 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/updater/operations/update_all_versions.rb:39:in `each'
updater | 2024/03/11 16:33:23 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/updater/operations/update_all_versions.rb:39:in `perform'
updater | 2024/03/11 16:33:23 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/updater.rb:45:in `run'
updater | 2024/03/11 16:33:23 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/update_files_command.rb:43:in `block in perform_job'
updater | 2024/03/11 16:33:23 ERROR <job_798517643> /home/dependabot/dependabot-updater/vendor/ruby/3.1.0/gems/opentelemetry-api-1.2.3/lib/opentelemetry/trace/tracer.rb:37:in `block in in_span'
updater | 2024/03/11 16:33:23 ERROR <job_798517643> /home/dependabot/dependabot-updater/vendor/ruby/3.1.0/gems/opentelemetry-api-1.2.3/lib/opentelemetry/trace.rb:70:in `block in with_span'
updater | 2024/03/11 16:33:23 ERROR <job_798517643> /home/dependabot/dependabot-updater/vendor/ruby/3.1.0/gems/opentelemetry-api-1.2.3/lib/opentelemetry/context.rb:87:in `with_value'
updater | 2024/03/11 16:33:23 ERROR <job_798517643> /home/dependabot/dependabot-updater/vendor/ruby/3.1.0/gems/opentelemetry-api-1.2.3/lib/opentelemetry/trace.rb:70:in `with_span'
updater | 2024/03/11 16:33:23 ERROR <job_798517643> /home/dependabot/dependabot-updater/vendor/ruby/3.1.0/gems/opentelemetry-api-1.2.3/lib/opentelemetry/trace/tracer.rb:37:in `in_span'
updater | 2024/03/11 16:33:23 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/update_files_command.rb:17:in `perform_job'
updater | 2024/03/11 16:33:23 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/base_command.rb:36:in `run'
updater | 2024/03/11 16:33:23 ERROR <job_798517643> bin/update_files.rb:24:in `<main>'
updater | 2024/03/11 16:33:23 INFO <job_798517643> Checking if AWSSDK.DynamoDBv2 3.7.301.18 needs updating
  proxy | 2024/03/11 16:33:23 [182] GET https://api.nuget.org:443/v3-flatcontainer/awssdk.dynamodbv2/3.7.301.18/awssdk.dynamodbv2.nuspec
  proxy | 2024/03/11 16:33:23 [182] 200 https://api.nuget.org:443/v3-flatcontainer/awssdk.dynamodbv2/3.7.301.18/awssdk.dynamodbv2.nuspec
  proxy | 2024/03/11 16:33:23 [184] GET https://api.nuget.org:443/v3-flatcontainer/awssdk.dynamodbv2/3.7.301.18/awssdk.dynamodbv2.3.7.301.18.nupkg
  proxy | 2024/03/11 16:33:23 [184] 200 https://api.nuget.org:443/v3-flatcontainer/awssdk.dynamodbv2/3.7.301.18/awssdk.dynamodbv2.3.7.301.18.nupkg
  proxy | 2024/03/11 16:33:24 [186] GET https://api.nuget.org:443/v3-flatcontainer/awssdk.dynamodbv2/3.7.301.19/awssdk.dynamodbv2.nuspec
  proxy | 2024/03/11 16:33:24 [186] 200 https://api.nuget.org:443/v3-flatcontainer/awssdk.dynamodbv2/3.7.301.19/awssdk.dynamodbv2.nuspec
  proxy | 2024/03/11 16:33:24 [188] GET https://api.nuget.org:443/v3-flatcontainer/awssdk.dynamodbv2/3.7.301.19/awssdk.dynamodbv2.3.7.301.19.nupkg
  proxy | 2024/03/11 16:33:24 [188] 200 https://api.nuget.org:443/v3-flatcontainer/awssdk.dynamodbv2/3.7.301.19/awssdk.dynamodbv2.3.7.301.19.nupkg
updater | 2024/03/11 16:33:24 INFO <job_798517643> Latest version is 3.7.301.19
updater | 2024/03/11 16:33:24 INFO <job_798517643> Requirements to unlock all
updater | 2024/03/11 16:33:24 INFO <job_798517643> Requirements update strategy 
updater | Finding updated dependencies for AWSSDK.DynamoDBv2.
  proxy | 2024/03/11 16:33:24 [190] GET https://api.nuget.org:443/v3-flatcontainer/awssdk.dynamodbv2/3.7.301.19/awssdk.dynamodbv2.nuspec
  proxy | 2024/03/11 16:33:24 [190] 200 https://api.nuget.org:443/v3-flatcontainer/awssdk.dynamodbv2/3.7.301.19/awssdk.dynamodbv2.nuspec
updater | 2024/03/11 16:33:24 INFO <job_798517643> Updating AWSSDK.DynamoDBv2 from 3.7.301.18 to 3.7.301.19
updater | running NuGet updater:
updater | /opt/nuget/NuGetUpdater/NuGetUpdater.Cli update --repo-root /home/dependabot/dependabot-updater/repo --solution-or-project /home/dependabot/dependabot-updater/repo/src/SomeProject/SomeProject.csproj --dependency AWSSDK.DynamoDBv2 --new-version 3.7.301.19 --previous-version 3.7.301.18 --verbose
updater | 2024/03/11 16:33:24 ERROR <job_798517643> Block argument of NuGetConfigCredentialHelpers::patch_nuget_config_for_action causes an exception A compatible .NET SDK was not found.
updater | 
updater | Requested SDK version: 8.0.201
updater | global.json file: /home/dependabot/dependabot-updater/repo/global.json
updater | 
updater | Installed SDKs:
updater | 
updater | Install the [8.0.201] .NET SDK or update [/home/dependabot/dependabot-updater/repo/global.json] to match an installed SDK.
updater | 
updater | Learn about SDK resolution:
updater | https://aka.ms/dotnet/sdk-not-found
updater | Unhandled exception: System.TypeInitializationException: The type initializer for 'NuGetUpdater.Core.MSBuildHelper' threw an exception.
updater |  ---> System.InvalidOperationException: Failed to find all versions of .NET Core MSBuild. Call to hostfxr_resolve_sdk2. There may be more details in stderr.
updater |    at Microsoft.Build.Locator.DotNetSdkLocationHelper.GetSdkFromGlobalSettings(String workingDirectory)
updater |    at Microsoft.Build.Locator.DotNetSdkLocationHelper.GetDotNetBasePaths(String workingDirectory)+MoveNext()
updater |    at Microsoft.Build.Locator.DotNetSdkLocationHelper.GetInstances(String workingDirectory)+MoveNext()
updater |    at Microsoft.Build.Locator.MSBuildLocator.GetInstances(VisualStudioInstanceQueryOptions options)+MoveNext()
updater |    at System.Linq.Enumerable.WhereEnumerableIterator`1.MoveNext()
updater |    at System.Linq.Enumerable.TryGetFirst[TSource](IEnumerable`1 source, Boolean& found)
updater |    at System.Linq.Enumerable.First[TSource](IEnumerable`1 source)
updater |    at NuGetUpdater.Core.MSBuildHelper.RegisterMSBuild() in /opt/nuget/lib/NuGetUpdater/NuGetUpdater.Core/Utilities/MSBuildHelper.cs:line 42
updater |    at NuGetUpdater.Core.MSBuildHelper..cctor() in /opt/nuget/lib/NuGetUpdater/NuGetUpdater.Core/Utilities/MSBuildHelper.cs:line 34
updater |    --- End of inner exception stack trace ---
updater |    at NuGetUpdater.Core.MSBuildHelper.RegisterMSBuild() in /opt/nuget/lib/NuGetUpdater/NuGetUpdater.Core/Utilities/MSBuildHelper.cs:line 40
updater |    at NuGetUpdater.Core.UpdaterWorker.RunAsync(String repoRootPath, String workspacePath, String dependencyName, String previousDependencyVersion, String newDependencyVersion, Boolean isTransitive) in /opt/nuget/lib/NuGetUpdater/NuGetUpdater.Core/Updater/UpdaterWorker.cs:line 22
updater |    at NuGetUpdater.Cli.Commands.UpdateCommand.<>c__DisplayClass7_0.<<GetCommand>b__0>d.MoveNext() in /opt/nuget/lib/NuGetUpdater/NuGetUpdater.Cli/Commands/UpdateCommand.cs:line 37
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Invocation.AnonymousCommandHandler.InvokeAsync(InvocationContext context)
updater |    at System.CommandLine.Invocation.InvocationPipeline.<>c__DisplayClass4_0.<<BuildInvocationChain>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass17_0.<<UseParseErrorReporting>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass12_0.<<UseHelp>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass22_0.<<UseVersionOption>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass19_0.<<UseTypoCorrections>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c.<<UseSuggestDirective>b__18_0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass16_0.<<UseParseDirective>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c.<<RegisterWithDotnetSuggest>b__5_0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass8_0.<<UseExceptionHandler>b__0>d.MoveNext()
updater | 8.0.100 [/usr/local/dotnet/current/sdk]:
updater | A compatible .NET SDK was not found.
updater | 
updater | Requested SDK version: 8.0.201
updater | global.json file: /home/dependabot/dependabot-updater/repo/global.json
updater | 
updater | Installed SDKs:
updater | 
updater | Install the [8.0.201] .NET SDK or update [/home/dependabot/dependabot-updater/repo/global.json] to match an installed SDK.
updater | 
updater | Learn about SDK resolution:
updater | https://aka.ms/dotnet/sdk-not-found
updater | Unhandled exception: System.TypeInitializationException: The type initializer for 'NuGetUpdater.Core.MSBuildHelper' threw an exception.
updater |  ---> System.InvalidOperationException: Failed to find all versions of .NET Core MSBuild. Call to hostfxr_resolve_sdk2. There may be more details in stderr.
updater |    at Microsoft.Build.Locator.DotNetSdkLocationHelper.GetSdkFromGlobalSettings(String workingDirectory)
updater |    at Microsoft.Build.Locator.DotNetSdkLocationHelper.GetDotNetBasePaths(String workingDirectory)+MoveNext()
updater |    at Microsoft.Build.Locator.DotNetSdkLocationHelper.GetInstances(String workingDirectory)+MoveNext()
updater |    at Microsoft.Build.Locator.MSBuildLocator.GetInstances(VisualStudioInstanceQueryOptions options)+MoveNext()
updater |    at System.Linq.Enumerable.WhereEnumerableIterator`1.MoveNext()
updater |    at System.Linq.Enumerable.TryGetFirst[TSource](IEnumerable`1 source, Boolean& found)
updater |    at System.Linq.Enumerable.First[TSource](IEnumerable`1 source)
updater |    at NuGetUpdater.Core.MSBuildHelper.RegisterMSBuild() in /opt/nuget/lib/NuGetUpdater/NuGetUpdater.Core/Utilities/MSBuildHelper.cs:line 42
updater |    at NuGetUpdater.Core.MSBuildHelper..cctor() in /opt/nuget/lib/NuGetUpdater/NuGetUpdater.Core/Utilities/MSBuildHelper.cs:line 34
updater |    --- End of inner exception stack trace ---
updater |    at NuGetUpdater.Core.MSBuildHelper.RegisterMSBuild() in /opt/nuget/lib/NuGetUpdater/NuGetUpdater.Core/Utilities/MSBuildHelper.cs:line 40
updater |    at NuGetUpdater.Core.UpdaterWorker.RunAsync(String repoRootPath, String workspacePath, String dependencyName, String previousDependencyVersion, String newDependencyVersion, Boolean isTransitive) in /opt/nuget/lib/NuGetUpdater/NuGetUpdater.Core/Updater/UpdaterWorker.cs:line 22
updater |    at NuGetUpdater.Cli.Commands.UpdateCommand.<>c__DisplayClass7_0.<<GetCommand>b__0>d.MoveNext() in /opt/nuget/lib/NuGetUpdater/NuGetUpdater.Cli/Commands/UpdateCommand.cs:line 37
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Invocation.AnonymousCommandHandler.InvokeAsync(InvocationContext context)
updater |    at System.CommandLine.Invocation.InvocationPipeline.<>c__DisplayClass4_0.<<BuildInvocationChain>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass17_0.<<UseParseErrorReporting>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass12_0.<<UseHelp>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass22_0.<<UseVersionOption>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass19_0.<<UseTypoCorrections>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c.<<UseSuggestDirective>b__18_0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass16_0.<<UseParseDirective>b__0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c.<<RegisterWithDotnetSuggest>b__5_0>d.MoveNext()
updater | --- End of stack trace from previous location ---
updater |    at System.CommandLine.Builder.CommandLineBuilderExtensions.<>c__DisplayClass8_0.<<UseExceptionHandler>b__0>d.MoveNext()
updater | 8.0.100 [/usr/local/dotnet/current/sdk]
updater | 
updater | 2024/03/11 16:33:25 ERROR <job_798517643> Error processing AWSSDK.DynamoDBv2 (Dependabot::DependabotError)
updater | 2024/03/11 16:33:25 ERROR <job_798517643> FileUpdater failed
updater | 2024/03/11 16:33:25 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/dependency_change_builder.rb:69:in `run'
updater | 2024/03/11 16:33:25 ERROR <job_798517643> /home/dependabot/dependabot-updater/vendor/ruby/3.1.0/gems/sorbet-runtime-0.5.11193/lib/types/private/methods/call_validation_2_7.rb:59:in `bind_call'
updater | 2024/03/11 16:33:25 ERROR <job_798517643> /home/dependabot/dependabot-updater/vendor/ruby/3.1.0/gems/sorbet-runtime-0.5.11193/lib/types/private/methods/call_validation_2_7.rb:59:in `block in create_validator_method_fast0'
updater | 2024/03/11 16:33:25 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/dependency_change_builder.rb:42:in `create_from'
updater | 2024/03/11 16:33:25 ERROR <job_798517643> /home/dependabot/dependabot-updater/vendor/ruby/3.1.0/gems/sorbet-runtime-0.5.11193/lib/types/private/methods/call_validation.rb:169:in `bind_call'
updater | 2024/03/11 16:33:25 ERROR <job_798517643> /home/dependabot/dependabot-updater/vendor/ruby/3.1.0/gems/sorbet-runtime-0.5.11193/lib/types/private/methods/call_validation.rb:169:in `validate_call_skip_block_type'
updater | 2024/03/11 16:33:25 ERROR <job_798517643> /home/dependabot/dependabot-updater/vendor/ruby/3.1.0/gems/sorbet-runtime-0.5.11193/lib/types/private/methods/call_validation.rb:111:in `block in create_validator_slow_skip_block_type'
updater | 2024/03/11 16:33:25 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/updater/operations/update_all_versions.rb:132:in `check_and_create_pull_request'
updater | 2024/03/11 16:33:25 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/updater/operations/update_all_versions.rb:64:in `check_and_create_pr_with_error_handling'
updater | 2024/03/11 16:33:25 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/updater/operations/update_all_versions.rb:39:in `block in perform'
updater | 2024/03/11 16:33:25 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/updater/operations/update_all_versions.rb:39:in `each'
updater | 2024/03/11 16:33:25 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/updater/operations/update_all_versions.rb:39:in `perform'
updater | 2024/03/11 16:33:25 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/updater.rb:45:in `run'
updater | 2024/03/11 16:33:25 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/update_files_command.rb:43:in `block in perform_job'
updater | 2024/03/11 16:33:25 ERROR <job_798517643> /home/dependabot/dependabot-updater/vendor/ruby/3.1.0/gems/opentelemetry-api-1.2.3/lib/opentelemetry/trace/tracer.rb:37:in `block in in_span'
updater | 2024/03/11 16:33:25 ERROR <job_798517643> /home/dependabot/dependabot-updater/vendor/ruby/3.1.0/gems/opentelemetry-api-1.2.3/lib/opentelemetry/trace.rb:70:in `block in with_span'
updater | 2024/03/11 16:33:25 ERROR <job_798517643> /home/dependabot/dependabot-updater/vendor/ruby/3.1.0/gems/opentelemetry-api-1.2.3/lib/opentelemetry/context.rb:87:in `with_value'
updater | 2024/03/11 16:33:25 ERROR <job_798517643> /home/dependabot/dependabot-updater/vendor/ruby/3.1.0/gems/opentelemetry-api-1.2.3/lib/opentelemetry/trace.rb:70:in `with_span'
updater | 2024/03/11 16:33:25 ERROR <job_798517643> /home/dependabot/dependabot-updater/vendor/ruby/3.1.0/gems/opentelemetry-api-1.2.3/lib/opentelemetry/trace/tracer.rb:37:in `in_span'
updater | 2024/03/11 16:33:25 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/update_files_command.rb:17:in `perform_job'
updater | 2024/03/11 16:33:25 ERROR <job_798517643> /home/dependabot/dependabot-updater/lib/dependabot/base_command.rb:36:in `run'
updater | 2024/03/11 16:33:25 ERROR <job_798517643> bin/update_files.rb:24:in `<main>'
updater | 2024/03/11 16:33:25 INFO <job_798517643> Finished job processing
updater | 2024/03/11 16:33:25 INFO Results:
updater | Dependabot encountered '3' error(s) during execution, please check the logs for more details.
updater | +-----------------------------------+
updater | |   Dependencies failed to update   |
updater | +-------------------+---------------+
updater | | AWSSDK.Core       | unknown_error |
updater | | AWSSDK.S3         | unknown_error |
updater | | AWSSDK.DynamoDBv2 | unknown_error |
updater | +-------------------+---------------+
updater | time="2024-03-11T16:33:25Z" level=info msg="task complete" container_id=job-798517643-updater exit_code=0 job_id=798517643 step=updater
```
