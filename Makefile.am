# Copyright (c) 2015 Cisco and/or its affiliates.
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at:
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

AUTOMAKE_OPTIONS = foreign subdir-objects

AM_CFLAGS = -Wall -I@TOOLKIT_INCLUDE@ -g

lib_LTLIBRARIES = ctrlcap_plugin.la ctrlcap_test_plugin.la
ctrlcap_plugin_la_SOURCES = ctrlcap/ctrlcap.c ctrlcap/punt_node.c ctrlcap/inject_node.c \
	ctrlcap/ctrlcap_plugin.api.h 
ctrlcap_plugin_la_LDFLAGS = -module

BUILT_SOURCES = ctrlcap/ctrlcap.api.h

SUFFIXES = .api.h .api

%.api.h: %.api
	mkdir -p `dirname $@` ; \
	$(CC) $(CPPFLAGS) -E -P -C -x c $^ \
	| vppapigen --input - --output $@ --show-name $@

nobase_include_HEADERS =			\
  ctrlcap/ctrlcap_all_api_h.h			\
  ctrlcap/ctrlcap_msg_enum.h			\
  ctrlcap/ctrlcap.api.h

ctrlcap_test_plugin_la_SOURCES = ctrlcap/ctrlcap_test.c ctrlcap/ctrlcap_plugin.api.h
ctrlcap_test_plugin_la_LDFLAGS = -module

if WITH_PLUGIN_TOOLKIT
install-data-hook:
	mkdir /usr/lib/vpp_plugins || true
	mkdir /usr/lib/vpp_api_test_plugins || true
	cp $(prefix)/lib/ctrlcap_plugin.so.*.*.* /usr/lib/vpp_plugins
	cp $(prefix)/lib/ctrlcap_test_plugin.so.*.*.* \
		/usr/lib/vpp_api_test_plugins
endif
