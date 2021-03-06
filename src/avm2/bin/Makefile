# Copyright 2013 Mozilla Foundation
#
# Licensed under the Apache License, Version 2.0 (the "License");
# you may not use this file except in compliance with the License.
# You may obtain a copy of the License at
#
#     http://www.apache.org/licenses/LICENSE-2.0
#
# Unless required by applicable law or agreed to in writing, software
# distributed under the License is distributed on an "AS IS" BASIS,
# WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
# See the License for the specific language governing permissions and
# limitations under the License.

AVM2_HOME = ..
UTILS_HOME = ../../../utils
AVM ?= $(UTILS_HOME)/tamarin-redux/bin/shell/avmshell
SHELLABC ?= $(AVM2_HOME)/gnerated/shell/shell.abc
BUILTINABC ?= $(AVM2_HOME)/generated/builtin/builtin.abc
ASC ?= $(UTILS_HOME)/asc.jar
JSSHELL ?= $(UTILS_HOME)/jsshell/js
THREADS ?= 8
TIMEOUT ?= 30000

NODE_MODULES = ../../../utils/node_modules

TEST_CMD = ASC=$(ASC) AVM=$(AVM) BUILTINABC=$(BUILTINABC) SHELLABC=$(SHELLABC) JSSHELL=$(JSSHELL) NODE_PATH=$(NODE_MODULES) node numbers.js -j $(THREADS) -t $(TIMEOUT) -jo

TEST_PATH ?= $(error Specify TEST_PATH variable)

default:
	echo "run: make [hello-world|test-pypy|test-interpreter|test-compiler|test-all]"

hello-world:
	ASC=$(ASC) AVM=$(AVM) BUILTINABC=$(BUILTINABC) ./shu.py asc -builtin ../tests/hello-world.as
	$(JSSHELL) avm.js -x ../tests/hello-world.abc
	$(TEST_CMD) -i ../tests/hello-world.abc -c icv

test-pypy:
	$(TEST_CMD) -i pypy.i.passed -c ic

test-interpreter:
	$(TEST_CMD) -i $(TEST_PATH) -c i

test-compiler:
	$(TEST_CMD) -i $(TEST_PATH) -c c

test-interpreter-all:
	$(TEST_CMD) -i tamarin.i.passed -i sunspider.i.passed -i pypy.i.passed -c i -nm

test-all:
	$(TEST_CMD) -i tamarin.i.passed -i sunspider.i.passed -i pypy.i.passed -c icv -nm

test-regress:
	ASC=$(ASC) AVM=$(AVM) BUILTINABC=$(BUILTINABC) ./shu.py reg
	$(TEST_CMD) -i ../tests/regress -e regress.disabled -c icv

.PHONY: default hello-world test-pypy test-interpreter test-compiler test-all
