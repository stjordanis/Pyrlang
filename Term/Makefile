PYPATH_SET=PYTHONPATH=$(ROOT)
LIBNAME=native_codec_impl
ROOT=$(shell pwd)
PY=PYTHONPATH=$(ROOT):$(ROOT)/target/debug python3

.PHONY: compile
compile:
	cargo build && \
	ln -fs $(ROOT)/target/debug/lib$(LIBNAME).so $(ROOT)/target/debug/$(LIBNAME).so
# && cargo build --release

.PHONY: clearterminal
clearterminal:
	clear && printf '\e[3J'

.PHONY: test
test: clearterminal compile
	for f in $(shell ls test/*_test.py); do \
		echo "RUNNING $$f"; \
		$(PY) $$f || exit 1; \
	done

.PHONY: clearterminal dtest
dtest: compile
	PYTHONPATH=$(ROOT):$(ROOT)/target/debug gdb --args python3 test/etf_decode_test.py

.PHONY: docs
docs:
	cd docs && $(PYPATH_SET) $(MAKE) html
