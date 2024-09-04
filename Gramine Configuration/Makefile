all: bow.manifest.sgx bow.sig

bow.manifest: manifest.template
	gramine-manifest \
		-Darch_libdir="/lib/x86_64-linux-gnu/" \
		-Dths=$(ths) \
		$< >$@

bow.manifest.sgx bow.sig: sgx_sign
	@:

.INTERMEDIATE: sgx_sign
sgx_sign: bow.manifest
	gramine-sgx-sign \
		--manifest $< \
		--output $<.sgx