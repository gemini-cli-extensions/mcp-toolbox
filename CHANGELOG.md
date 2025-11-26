# Changelog

## [0.3.0](https://github.com/gemini-cli-extensions/mcp-toolbox/compare/0.2.1...0.3.0) (2025-11-26)


### ⚠ BREAKING CHANGES

* **tools/spanner-list-tables:** Unmarshal `object_details` json string into map to make response have nested json ([genai-toolbox#​1894](https://redirect.github.com/googleapis/genai-toolbox/issues/1894)) ([446d62a](https://redirect.github.com/googleapis/genai-toolbox/commit/446d62acd995d5128f52e9db254dd1c7138227c6))

### Features

* **tools/postgres:** Add `long_running_transactions`, `list_locks` and `replication_stats` tools ([genai-toolbox#​1751](https://redirect.github.com/googleapis/genai-toolbox/issues/1751)) ([5abad5d](https://redirect.github.com/googleapis/genai-toolbox/commit/5abad5d56c6cc5ba86adc5253b948bf8230fa830)) ([a40592c](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a40592cba476ea3c5b131429da3d6b8efe6b1f12))
* **tools/spanner-list-tables:** Unmarshal `object_details` json string into map to make response have nested json ([genai-toolbox#​1894](https://redirect.github.com/googleapis/genai-toolbox/issues/1894)) ([446d62a](https://redirect.github.com/googleapis/genai-toolbox/commit/446d62acd995d5128f52e9db254dd1c7138227c6)) ([a40592c](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a40592cba476ea3c5b131429da3d6b8efe6b1f12))


### Bug Fixes

* **tools:** Check for query execution error for pgxpool.Pool ([genai-toolbox#​1969](https://redirect.github.com/googleapis/genai-toolbox/issues/1969)) ([2bff138](https://redirect.github.com/googleapis/genai-toolbox/commit/2bff1384a3570ef46bc03ebebc507923af261987)) ([a40592c](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a40592cba476ea3c5b131429da3d6b8efe6b1f12))
* **tools/alloydbgetinstance:** Remove parameter duplication ([genai-toolbox#​1993](https://redirect.github.com/googleapis/genai-toolbox/issues/1993)) ([0e269a1](https://redirect.github.com/googleapis/genai-toolbox/commit/0e269a1d125eed16a51ead27db4398e6e48cb948)) ([a40592c](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a40592cba476ea3c5b131429da3d6b8efe6b1f12))

## [0.2.1](https://github.com/gemini-cli-extensions/mcp-toolbox/compare/0.2.0...0.2.1) (2025-11-14)


### Features

* **source/alloydb, source/cloud-sql-postgres,source/cloud-sql-mysql,source/cloud-sql-mssql:** Use project from env for alloydb and cloud sql control plane tools ([genai-toolbox#​1588](https://redirect.github.com/googleapis/genai-toolbox/issues/1588)) ([12bdd95](https://redirect.github.com/googleapis/genai-toolbox/commit/12bdd954597e49d3ec6b247cc104584c5a4d1943)) ([e57d7a4](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/e57d7a40732ed7ca592f6415a96d79ea3ebddc08))
* **source/mysql:** Set default host and port for MySQL source ([genai-toolbox#​1922](https://redirect.github.com/googleapis/genai-toolbox/issues/1922)) ([2c228ef](https://redirect.github.com/googleapis/genai-toolbox/commit/2c228ef4f2d4cb8dfc41e845466bfe3566d141a1)) ([e57d7a4](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/e57d7a40732ed7ca592f6415a96d79ea3ebddc08))
* **source/Postgresql:** Set default host and port for Postgresql  source ([genai-toolbox#​1927](https://redirect.github.com/googleapis/genai-toolbox/issues/1927)) ([7e6e88a](https://redirect.github.com/googleapis/genai-toolbox/commit/7e6e88a21f2b9b60e0d645cdde33a95892d31a04)) ([e57d7a4](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/e57d7a40732ed7ca592f6415a96d79ea3ebddc08))
* **tool/looker-generate-embed-url:** Adding generate embed url tool ([genai-toolbox#​1877](https://redirect.github.com/googleapis/genai-toolbox/issues/1877)) ([ef63860](https://redirect.github.com/googleapis/genai-toolbox/commit/ef63860559798fbad54c1051d9f53bce42d66464)) ([e57d7a4](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/e57d7a40732ed7ca592f6415a96d79ea3ebddc08))
* **tools/postgres:** Add `list_triggers`, `database_overview` tools for postgres ([genai-toolbox#​1912](https://redirect.github.com/googleapis/genai-toolbox/issues/1912)) ([a4c9287](https://redirect.github.com/googleapis/genai-toolbox/commit/a4c9287aecf848faa98d973a9ce5b13fa309a58e)) ([e57d7a4](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/e57d7a40732ed7ca592f6415a96d79ea3ebddc08))
* **tools/postgres:** Add list\_indexes, list\_sequences tools for postgres ([genai-toolbox#​1765](https://redirect.github.com/googleapis/genai-toolbox/issues/1765)) ([897c63d](https://redirect.github.com/googleapis/genai-toolbox/commit/897c63dcea43226262d2062088c59f2d1068fca7)) ([e57d7a4](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/e57d7a40732ed7ca592f6415a96d79ea3ebddc08))
* Added prompt support for toolbox ([genai-toolbox#​1798](https://redirect.github.com/googleapis/genai-toolbox/issues/1798)) ([cd56ea4](https://redirect.github.com/googleapis/genai-toolbox/commit/cd56ea44fbdd149fcb92324e70ee36ac747635db)) ([e57d7a4](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/e57d7a40732ed7ca592f6415a96d79ea3ebddc08))

## [0.2.0](https://github.com/gemini-cli-extensions/mcp-toolbox/compare/0.1.3...0.2.0) (2025-11-07)


### ⚠ BREAKING CHANGES

* **tools/bigquery-analyze-contribution:** Add allowed dataset support ([genai-toolbox#​1675](https://redirect.github.com/googleapis/genai-toolbox/issues/1675)) ([ef28e39](https://redirect.github.com/googleapis/genai-toolbox/commit/ef28e39e90b21287ca8e69b99f4e792c78e9d31f))
* **tools/bigquery-get-dataset-info:** add allowed dataset support ([genai-toolbox#​1654](https://redirect.github.com/googleapis/genai-toolbox/issues/1654))
* **tools/alloydbainl:** update AlloyDB AI NL statement order ([genai-toolbox#​1753](https://redirect.github.com/googleapis/genai-toolbox/issues/1753))

### Features

* **cloud-healthcare:** Add support for healthcare source, tool and prebuilt config ([genai-toolbox#​1853](https://redirect.github.com/googleapis/genai-toolbox/issues/1853)) ([1f833fb](https://redirect.github.com/googleapis/genai-toolbox/commit/1f833fb1a124e23819ddfec476f2e63ef31dd22f)) ([a7ed381](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a7ed3817af6bd2e5b6ae1f680c3fd92907811668))
* **elasticsearch:** Add Elasticsearch source and tools ([genai-toolbox#​1109](https://redirect.github.com/googleapis/genai-toolbox/issues/1109)) ([5367285](https://redirect.github.com/googleapis/genai-toolbox/commit/5367285e91ddda99ae7261d8ed4b025f975d1453)) ([a7ed381](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a7ed3817af6bd2e5b6ae1f680c3fd92907811668))
* **mindsdb:** Add MindsDB Source and Tools  ([genai-toolbox#​878](https://redirect.github.com/googleapis/genai-toolbox/issues/878)) ([1b2cca9](https://redirect.github.com/googleapis/genai-toolbox/commit/1b2cca9faa6f7bacbeb5d25634ce3bf61067de16)) ([a7ed381](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a7ed3817af6bd2e5b6ae1f680c3fd92907811668))
* **singlestore:** Add SingleStore Source and Tools ([genai-toolbox#​1333](https://redirect.github.com/googleapis/genai-toolbox/issues/1333)) ([40b9dba](https://redirect.github.com/googleapis/genai-toolbox/commit/40b9dbab088add05a66995abb1c71a9345b8f7e5)) ([a7ed381](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a7ed3817af6bd2e5b6ae1f680c3fd92907811668))
* **source/bigquery:** Add client cache for user-passed credentials ([genai-toolbox#​1119](https://redirect.github.com/googleapis/genai-toolbox/issues/1119)) ([cf7012a](https://redirect.github.com/googleapis/genai-toolbox/commit/cf7012a82bb5c77309da3a26e563a5015786aa69)) ([a7ed381](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a7ed3817af6bd2e5b6ae1f680c3fd92907811668))
* **source/bigquery:** Add service account impersonation support for bigquery ([genai-toolbox#​1641](https://redirect.github.com/googleapis/genai-toolbox/issues/1641)) ([e09d182](https://redirect.github.com/googleapis/genai-toolbox/commit/e09d182f88bf697a169428f477aebc9f1741e35f)) ([a7ed381](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a7ed3817af6bd2e5b6ae1f680c3fd92907811668))
* **tools/alloydbainl:** update AlloyDB AI NL statement order ([genai-toolbox#​1753](https://redirect.github.com/googleapis/genai-toolbox/issues/1753)) ([a7ed381](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a7ed3817af6bd2e5b6ae1f680c3fd92907811668))
* **tools/bigquery-analyze-contribution:** Add allowed dataset support ([genai-toolbox#​1675](https://redirect.github.com/googleapis/genai-toolbox/issues/1675)) ([ef28e39](https://redirect.github.com/googleapis/genai-toolbox/commit/ef28e39e90b21287ca8e69b99f4e792c78e9d31f)) ([a7ed381](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a7ed3817af6bd2e5b6ae1f680c3fd92907811668))
* **tools/bigquery-analyze-contribution:** Add allowed dataset support ([genai-toolbox#​1675](https://redirect.github.com/googleapis/genai-toolbox/issues/1675)) ([ef28e39](https://redirect.github.com/googleapis/genai-toolbox/commit/ef28e39e90b21287ca8e69b99f4e792c78e9d31f)) ([a7ed381](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a7ed3817af6bd2e5b6ae1f680c3fd92907811668))
* **tools/bigquery-get-dataset-info:** add allowed dataset support ([genai-toolbox#​1654](https://redirect.github.com/googleapis/genai-toolbox/issues/1654)) ([a7ed381](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a7ed3817af6bd2e5b6ae1f680c3fd92907811668))
* **tools/bigquery-get-dataset-info:** Add allowed dataset support ([genai-toolbox#​1654](https://redirect.github.com/googleapis/genai-toolbox/issues/1654)) ([a2006ad](https://redirect.github.com/googleapis/genai-toolbox/commit/a2006ad57718ebad3de5c6850e9c6a5a763808ec)) ([a7ed381](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a7ed3817af6bd2e5b6ae1f680c3fd92907811668))
* **tools/looker-run-dashboard:** New `run_dashboard` tool ([genai-toolbox#​1858](https://redirect.github.com/googleapis/genai-toolbox/issues/1858)) ([30857c2](https://redirect.github.com/googleapis/genai-toolbox/commit/30857c2294bb14961d3be49e2c368c69ecf844ec)) ([a7ed381](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a7ed3817af6bd2e5b6ae1f680c3fd92907811668))
* **tools/looker-run-look:** Modify run\_look to show query origin ([genai-toolbox#​1860](https://redirect.github.com/googleapis/genai-toolbox/issues/1860)) ([991e539](https://redirect.github.com/googleapis/genai-toolbox/commit/991e539f9c7978fa618ada3179a0b656c33ff501)) ([a7ed381](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a7ed3817af6bd2e5b6ae1f680c3fd92907811668))
* **tools/looker:** Tools to retrieve the connections, schemas, databases, and column metadata from a looker system. ([genai-toolbox#​1804](https://redirect.github.com/googleapis/genai-toolbox/issues/1804)) ([d7d1b03](https://redirect.github.com/googleapis/genai-toolbox/commit/d7d1b03f3b746ed748d67f67e833457d55c846ab)) ([a7ed381](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a7ed3817af6bd2e5b6ae1f680c3fd92907811668))
* **tools/mongodb:** Make MongoDB tools' `filterParams` field optional ([genai-toolbox#​1614](https://redirect.github.com/googleapis/genai-toolbox/issues/1614)) ([208ab92](https://redirect.github.com/googleapis/genai-toolbox/commit/208ab92eb377b538a99330a415ecc18790b077b7)) ([a7ed381](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a7ed3817af6bd2e5b6ae1f680c3fd92907811668))
* **tools/neo4j-execute-cypher:** Add dry\_run parameter to validate Cypher queries ([genai-toolbox#​1769](https://redirect.github.com/googleapis/genai-toolbox/issues/1769)) ([f475da6](https://redirect.github.com/googleapis/genai-toolbox/commit/f475da63ce1b65387b503ac497eca47635452723)) ([a7ed381](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a7ed3817af6bd2e5b6ae1f680c3fd92907811668))
* **tools/postgres-list-schemas:** Add new postgres-list-schemas tool ([genai-toolbox#​1741](https://redirect.github.com/googleapis/genai-toolbox/issues/1741)) ([1a19cac](https://redirect.github.com/googleapis/genai-toolbox/commit/1a19cac7cd89ed70291eb55e190370fe7b2c1aba)) ([a7ed381](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a7ed3817af6bd2e5b6ae1f680c3fd92907811668))
* **tools/postgres-list-views:** Add new postgres-list-views tool ([genai-toolbox#​1709](https://redirect.github.com/googleapis/genai-toolbox/issues/1709)) ([e8c7fe0](https://redirect.github.com/googleapis/genai-toolbox/commit/e8c7fe0994fedcb9be78d461fab3c98cc6bd86b2)) ([a7ed381](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a7ed3817af6bd2e5b6ae1f680c3fd92907811668))
* **tools/serverless-spark:** Add cancel-batch tool ([genai-toolbox#​1827](https://redirect.github.com/googleapis/genai-toolbox/pull/1827))([2881683](https://redirect.github.com/googleapis/genai-toolbox/commit/28816832265250de97d84e6ba38bf6c35e040796)) ([a7ed381](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a7ed3817af6bd2e5b6ae1f680c3fd92907811668))
* **tools/serverless-spark:** Add get\_batch tool ([genai-toolbox#​1783](https://redirect.github.com/googleapis/genai-toolbox/pull/1783))([7ad1072](https://redirect.github.com/googleapis/genai-toolbox/commit/7ad10720b4638324cd77d8aa410cbd1ccf0cc93f)) ([a7ed381](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a7ed3817af6bd2e5b6ae1f680c3fd92907811668))
* **tools/serverless-spark:** Add serverless-spark source with list\_batches tool ([genai-toolbox#​1690](https://redirect.github.com/googleapis/genai-toolbox/pull/1690))([816dbce](https://redirect.github.com/googleapis/genai-toolbox/commit/816dbce268392046e54767732bd31488c6e89bdb)) ([a7ed381](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a7ed3817af6bd2e5b6ae1f680c3fd92907811668))
* Support `excludeValues` for parameters ([genai-toolbox#​1818](https://redirect.github.com/googleapis/genai-toolbox/issues/1818)) ([a8e98dc](https://redirect.github.com/googleapis/genai-toolbox/commit/a8e98dc99d208e8b37a3bc4d1ab4749b5154ed36)) ([a7ed381](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a7ed3817af6bd2e5b6ae1f680c3fd92907811668))


### Bug Fixes

* **cloudmonitoring:** Populate `authRequired` in tool manifest ([genai-toolbox#​1800](https://redirect.github.com/googleapis/genai-toolbox/issues/1800)) ([954152c](https://redirect.github.com/googleapis/genai-toolbox/commit/954152c7928bf0da9be221e011e32f74bc4cebbc)) ([a7ed381](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a7ed3817af6bd2e5b6ae1f680c3fd92907811668))
* **source/cloud-sql-mssql:** Remove `ipAddress` field ([genai-toolbox#​1822](https://redirect.github.com/googleapis/genai-toolbox/issues/1822)) ([38d535d](https://redirect.github.com/googleapis/genai-toolbox/commit/38d535de34cfedd6828a01d9dcd25daf1bad7306)) ([a7ed381](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a7ed3817af6bd2e5b6ae1f680c3fd92907811668))
* **tools/alloydbainl:** AlloyDB AI NL execute\_sql statement order ([genai-toolbox#​1753](https://redirect.github.com/googleapis/genai-toolbox/issues/1753)) ([9723cad](https://redirect.github.com/googleapis/genai-toolbox/commit/9723cadaa181a76d8fdda65a6254f6c887c3cf57)) ([a7ed381](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a7ed3817af6bd2e5b6ae1f680c3fd92907811668))
* **tools/postgres-execute-sql:** Do not ignore SQL failure ([genai-toolbox#​1829](https://redirect.github.com/googleapis/genai-toolbox/issues/1829)) ([8984287](https://redirect.github.com/googleapis/genai-toolbox/commit/898428759c2a1a384bea8939605cf0914d129bec)) ([a7ed381](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a7ed3817af6bd2e5b6ae1f680c3fd92907811668))
* Bigquery execute\_sql to assign values to array ([genai-toolbox#​1884](https://redirect.github.com/googleapis/genai-toolbox/issues/1884)) ([559e2a2](https://redirect.github.com/googleapis/genai-toolbox/commit/559e2a22e0db20bb947702e13140ce869b5865a7)) ([a7ed381](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a7ed3817af6bd2e5b6ae1f680c3fd92907811668))
* Instructions to quote filters that include commas ([genai-toolbox#​1794](https://redirect.github.com/googleapis/genai-toolbox/issues/1794)) ([4b01720](https://redirect.github.com/googleapis/genai-toolbox/commit/4b0172083c0dd4c71098d4e0ab5fa0b16ea0d830)) ([a7ed381](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a7ed3817af6bd2e5b6ae1f680c3fd92907811668))
* Update debug logs statements ([genai-toolbox#​1828](https://redirect.github.com/googleapis/genai-toolbox/issues/1828)) ([3cff915](https://redirect.github.com/googleapis/genai-toolbox/commit/3cff915e22c3a5e4e296607f83ae6409b896c9a9)) ([a7ed381](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/a7ed3817af6bd2e5b6ae1f680c3fd92907811668))

## [0.1.3](https://github.com/gemini-cli-extensions/mcp-toolbox/compare/0.1.2...0.1.3) (2025-10-27)


### Features

* **tools/looker:** Tools to allow the agent to retrieve, create, modify, and delete LookML project files. ([#1673](https://redirect.github.com/googleapis/genai-toolbox/issues/1673)) ([089081f](https://redirect.github.com/googleapis/genai-toolbox/commit/089081feb0e32f9eb65d00df5987392d413a4081)) ([f006c4c](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/f006c4c765c91f678e7055c55e43828e60962da6))
* Support `allowedValues`, `escape`, `minValue` and `maxValue` for parameters ([#1770](https://redirect.github.com/googleapis/genai-toolbox/issues/1770)) ([eaf7740](https://redirect.github.com/googleapis/genai-toolbox/commit/eaf77406fd386c12315d67eb685dc69e0415c516)) ([f006c4c](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/f006c4c765c91f678e7055c55e43828e60962da6))


### Bug Fixes

* **sources/mysql:** Escape mysql user agent ([#1707](https://redirect.github.com/googleapis/genai-toolbox/issues/1707)) ([eeb694c](https://redirect.github.com/googleapis/genai-toolbox/commit/eeb694c20facc40a38bfa67073c4cb1f3dd657ff)) ([f006c4c](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/f006c4c765c91f678e7055c55e43828e60962da6))
* **sources/mysql:** Escape program\_name for MySQL ([#1717](https://redirect.github.com/googleapis/genai-toolbox/issues/1717)) ([02f7f8a](https://redirect.github.com/googleapis/genai-toolbox/commit/02f7f8af979057efe99fd138cb1b958130355b68)) ([f006c4c](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/f006c4c765c91f678e7055c55e43828e60962da6))
* **tools/http:** Allow 2xx status code on tool invocation ([#1761](https://redirect.github.com/googleapis/genai-toolbox/issues/1761)) ([a06d0d8](https://redirect.github.com/googleapis/genai-toolbox/commit/a06d0d8735fbec29bea97457248845a8c6b4aa3c)) ([f006c4c](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/f006c4c765c91f678e7055c55e43828e60962da6))
* **tools/http:** Omit optional nil query parameters ([#1762](https://redirect.github.com/googleapis/genai-toolbox/issues/1762)) ([bd16ba3](https://redirect.github.com/googleapis/genai-toolbox/commit/bd16ba3921e6177065780e5f29870859b8e18e4f)) ([f006c4c](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/f006c4c765c91f678e7055c55e43828e60962da6))
* **tools/looker:** Looker file content calls should not use url.QueryEscape ([#1758](https://redirect.github.com/googleapis/genai-toolbox/issues/1758)) ([336de1b](https://redirect.github.com/googleapis/genai-toolbox/commit/336de1bd04b869d322c0fd1f4667eb652159d791)) ([f006c4c](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/f006c4c765c91f678e7055c55e43828e60962da6))

## [0.1.2](https://github.com/gemini-cli-extensions/mcp-toolbox/compare/0.1.1...0.1.2) (2025-10-17)


### Features

* **deps:** update dependency googleapis/genai-toolbox to v0.17.0 ([#33](https://github.com/gemini-cli-extensions/mcp-toolbox/issues/33)) ([5745a8f](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/5745a8fc96336cbedc3d99cdecaedd2721ea6ce5))

## [0.1.1](https://github.com/gemini-cli-extensions/mcp-toolbox/compare/0.1.0...0.1.1) (2025-09-30)


### Features

* additional instructions for the context file ([#25](https://github.com/gemini-cli-extensions/mcp-toolbox/issues/25)) ([1413efc](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/1413efcd66b03224705429eefdfb58e4ebf79f40))
* standardize mcp server names ([#23](https://github.com/gemini-cli-extensions/mcp-toolbox/issues/23)) ([e58b860](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/e58b86093975ddbbad5de7c1382a73187fa66117))

## 0.1.0 (2025-09-21)


### Miscellaneous Chores

* make binary executable ([#7](https://github.com/gemini-cli-extensions/mcp-toolbox/issues/7)) ([e15c109](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/e15c109a8b91b826d63cab634777d831c147879f))
* release 0.1.0 ([#6](https://github.com/gemini-cli-extensions/mcp-toolbox/issues/6)) ([6186ee5](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/6186ee50ecf689c037a297d84816fa8b39b5314a))
* update codeowners ([#4](https://github.com/gemini-cli-extensions/mcp-toolbox/issues/4)) ([ed127cf](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/ed127cfcf07f45287f38d8d0212e4b86274fa32a))


### Documentation

* Update gemini-extension.json ([#1](https://github.com/gemini-cli-extensions/mcp-toolbox/issues/1)) ([3395560](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/3395560c7382727f5a006cc08de6ec91256e8286))
* update readme to remove disclaimer and update context file ([#2](https://github.com/gemini-cli-extensions/mcp-toolbox/issues/2)) ([02adcb2](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/02adcb2a0844c7f23dd1e42259a033edec08a814))
* Update README.md ([#5](https://github.com/gemini-cli-extensions/mcp-toolbox/issues/5)) ([9996d10](https://github.com/gemini-cli-extensions/mcp-toolbox/commit/9996d105887d7c09ab58ce54419c98bcc4e0f655))
