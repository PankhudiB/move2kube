#   Copyright IBM Corporation 2020
#
#   Licensed under the Apache License, Version 2.0 (the "License");
#   you may not use this file except in compliance with the License.
#   You may obtain a copy of the License at
#
#        http://www.apache.org/licenses/LICENSE-2.0
#
#   Unless required by applicable law or agreed to in writing, software
#   distributed under the License is distributed on an "AS IS" BASIS,
#   WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
#   See the License for the specific language governing permissions and
#   limitations under the License.

# Build App
FROM registry.access.redhat.com/ubi8/ubi:latest AS build_base
RUN yum install -y java-1.8.0-openjdk-devel
RUN yum install -y maven
COPY . /{{.APPNAME}}
WORKDIR /{{.APPNAME}}
RUN mvn package

# Run App
FROM registry.access.redhat.com/jboss-eap-6/eap64-openshift:latest
EXPOSE {{.Port}}
COPY --from=build_base /{{.APPNAME}}/target/* /opt/eap/standalone/deployments/