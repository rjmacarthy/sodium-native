cmake_minimum_required(VERSION 3.25)

project(sodium_native C ASM)

set(CMAKE_POSITION_INDEPENDENT_CODE ON)

include(TestBigEndian)

include(bare)
include(napi)

bare_target(target)

find_program(node NAMES node REQUIRED)

add_custom_command(
  COMMAND ${node} scripts/version.js
  WORKING_DIRECTORY ${PROJECT_SOURCE_DIR}
  OUTPUT
    ${PROJECT_SOURCE_DIR}/vendor/libsodium/src/libsodium/include/sodium/version.h
  DEPENDS
    vendor/libsodium/src/libsodium/include/sodium/version.h.in
  VERBATIM
)

add_library(sodium OBJECT)

target_sources(
  sodium
  INTERFACE
    vendor/libsodium/src/libsodium/include/sodium/private/chacha20_ietf_ext.h
    vendor/libsodium/src/libsodium/include/sodium/private/common.h
    vendor/libsodium/src/libsodium/include/sodium/core.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_aead_aes256gcm.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_aead_chacha20poly1305.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_aead_xchacha20poly1305.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_auth.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_auth_hmacsha256.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_auth_hmacsha512.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_auth_hmacsha512256.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_box.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_box_curve25519xchacha20poly1305.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_box_curve25519xsalsa20poly1305.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_core_ed25519.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_core_hchacha20.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_core_hsalsa20.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_core_ristretto255.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_core_salsa20.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_core_salsa208.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_core_salsa2012.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_generichash.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_generichash_blake2b.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_hash.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_hash_sha256.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_hash_sha512.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_kdf.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_kdf_blake2b.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_kx.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_onetimeauth.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_onetimeauth_poly1305.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_pwhash.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_pwhash_argon2i.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_pwhash_argon2id.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_pwhash_scryptsalsa208sha256.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_scalarmult.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_scalarmult_curve25519.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_scalarmult_ed25519.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_scalarmult_ristretto255.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_secretbox.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_secretbox_xchacha20poly1305.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_secretbox_xsalsa20poly1305.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_secretstream_xchacha20poly1305.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_shorthash.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_shorthash_siphash24.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_sign.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_sign_ed25519.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_sign_edwards25519sha512batch.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_stream.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_stream_chacha20.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_stream_salsa20.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_stream_salsa208.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_stream_salsa2012.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_stream_xchacha20.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_stream_xsalsa20.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_verify_16.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_verify_32.h
    vendor/libsodium/src/libsodium/include/sodium/crypto_verify_64.h
    vendor/libsodium/src/libsodium/include/sodium/private/ed25519_ref10.h
    vendor/libsodium/src/libsodium/include/sodium/private/ed25519_ref10_fe_25_5.h
    vendor/libsodium/src/libsodium/include/sodium/private/ed25519_ref10_fe_51.h
    vendor/libsodium/src/libsodium/include/sodium/export.h
    vendor/libsodium/src/libsodium/include/sodium/private/implementations.h
    vendor/libsodium/src/libsodium/include/sodium/private/mutex.h
    vendor/libsodium/src/libsodium/include/sodium/randombytes.h
    vendor/libsodium/src/libsodium/include/sodium/randombytes_internal_random.h
    vendor/libsodium/src/libsodium/include/sodium/randombytes_sysrandom.h
    vendor/libsodium/src/libsodium/include/sodium/runtime.h
    vendor/libsodium/src/libsodium/include/sodium.h
    vendor/libsodium/src/libsodium/include/sodium/private/sse2_64_32.h
    vendor/libsodium/src/libsodium/include/sodium/utils.h
  PUBLIC
    vendor/libsodium/src/libsodium/include/sodium/version.h
  PRIVATE
    vendor/libsodium/src/libsodium/crypto_aead/aes256gcm/aesni/aead_aes256gcm_aesni.c
    vendor/libsodium/src/libsodium/crypto_aead/chacha20poly1305/sodium/aead_chacha20poly1305.c
    vendor/libsodium/src/libsodium/crypto_aead/xchacha20poly1305/sodium/aead_xchacha20poly1305.c
    vendor/libsodium/src/libsodium/crypto_pwhash/argon2/argon2-core.c
    vendor/libsodium/src/libsodium/crypto_pwhash/argon2/argon2-encoding.c
    vendor/libsodium/src/libsodium/crypto_pwhash/argon2/argon2-fill-block-avx2.c
    vendor/libsodium/src/libsodium/crypto_pwhash/argon2/argon2-fill-block-avx512f.c
    vendor/libsodium/src/libsodium/crypto_pwhash/argon2/argon2-fill-block-ref.c
    vendor/libsodium/src/libsodium/crypto_pwhash/argon2/argon2-fill-block-ssse3.c
    vendor/libsodium/src/libsodium/crypto_pwhash/argon2/argon2.c
    vendor/libsodium/src/libsodium/crypto_auth/hmacsha256/auth_hmacsha256.c
    vendor/libsodium/src/libsodium/crypto_auth/hmacsha512/auth_hmacsha512.c
    vendor/libsodium/src/libsodium/crypto_auth/hmacsha512256/auth_hmacsha512256.c
    vendor/libsodium/src/libsodium/crypto_generichash/blake2b/ref/blake2b-compress-avx2.c
    vendor/libsodium/src/libsodium/crypto_generichash/blake2b/ref/blake2b-compress-ref.c
    vendor/libsodium/src/libsodium/crypto_generichash/blake2b/ref/blake2b-compress-sse41.c
    vendor/libsodium/src/libsodium/crypto_generichash/blake2b/ref/blake2b-compress-ssse3.c
    vendor/libsodium/src/libsodium/crypto_pwhash/argon2/blake2b-long.c
    vendor/libsodium/src/libsodium/crypto_generichash/blake2b/ref/blake2b-ref.c
    vendor/libsodium/src/libsodium/crypto_box/curve25519xchacha20poly1305/box_curve25519xchacha20poly1305.c
    vendor/libsodium/src/libsodium/crypto_box/curve25519xsalsa20poly1305/box_curve25519xsalsa20poly1305.c
    vendor/libsodium/src/libsodium/crypto_box/curve25519xchacha20poly1305/box_seal_curve25519xchacha20poly1305.c
    vendor/libsodium/src/libsodium/crypto_stream/chacha20/dolbeau/chacha20_dolbeau-avx2.c
    vendor/libsodium/src/libsodium/crypto_stream/chacha20/dolbeau/chacha20_dolbeau-ssse3.c
    vendor/libsodium/src/libsodium/crypto_stream/chacha20/ref/chacha20_ref.c
    vendor/libsodium/src/libsodium/sodium/codecs.c
    vendor/libsodium/src/libsodium/sodium/core.c
    vendor/libsodium/src/libsodium/crypto_core/ed25519/core_ed25519.c
    vendor/libsodium/src/libsodium/crypto_core/hchacha20/core_hchacha20.c
    vendor/libsodium/src/libsodium/crypto_core/hsalsa20/core_hsalsa20.c
    vendor/libsodium/src/libsodium/crypto_core/hsalsa20/ref2/core_hsalsa20_ref2.c
    vendor/libsodium/src/libsodium/crypto_core/ed25519/core_ristretto255.c
    vendor/libsodium/src/libsodium/crypto_core/salsa/ref/core_salsa_ref.c
    vendor/libsodium/src/libsodium/crypto_auth/crypto_auth.c
    vendor/libsodium/src/libsodium/crypto_box/crypto_box.c
    vendor/libsodium/src/libsodium/crypto_box/crypto_box_easy.c
    vendor/libsodium/src/libsodium/crypto_box/crypto_box_seal.c
    vendor/libsodium/src/libsodium/crypto_generichash/crypto_generichash.c
    vendor/libsodium/src/libsodium/crypto_hash/crypto_hash.c
    vendor/libsodium/src/libsodium/crypto_kdf/crypto_kdf.c
    vendor/libsodium/src/libsodium/crypto_kx/crypto_kx.c
    vendor/libsodium/src/libsodium/crypto_onetimeauth/crypto_onetimeauth.c
    vendor/libsodium/src/libsodium/crypto_pwhash/crypto_pwhash.c
    vendor/libsodium/src/libsodium/crypto_scalarmult/crypto_scalarmult.c
    vendor/libsodium/src/libsodium/crypto_pwhash/scryptsalsa208sha256/crypto_scrypt-common.c
    vendor/libsodium/src/libsodium/crypto_secretbox/crypto_secretbox.c
    vendor/libsodium/src/libsodium/crypto_secretbox/crypto_secretbox_easy.c
    vendor/libsodium/src/libsodium/crypto_shorthash/crypto_shorthash.c
    vendor/libsodium/src/libsodium/crypto_sign/crypto_sign.c
    vendor/libsodium/src/libsodium/crypto_stream/crypto_stream.c
    vendor/libsodium/src/libsodium/crypto_scalarmult/curve25519/sandy2x/curve25519_sandy2x.c
    vendor/libsodium/src/libsodium/crypto_core/ed25519/ref10/ed25519_ref10.c
    vendor/libsodium/src/libsodium/crypto_scalarmult/curve25519/sandy2x/fe51_invert.c
    vendor/libsodium/src/libsodium/crypto_scalarmult/curve25519/sandy2x/fe_frombytes_sandy2x.c
    vendor/libsodium/src/libsodium/crypto_generichash/blake2b/generichash_blake2.c
    vendor/libsodium/src/libsodium/crypto_generichash/blake2b/ref/generichash_blake2b.c
    vendor/libsodium/src/libsodium/crypto_hash/sha256/hash_sha256.c
    vendor/libsodium/src/libsodium/crypto_hash/sha256/cp/hash_sha256_cp.c
    vendor/libsodium/src/libsodium/crypto_hash/sha512/hash_sha512.c
    vendor/libsodium/src/libsodium/crypto_hash/sha512/cp/hash_sha512_cp.c
    vendor/libsodium/src/libsodium/crypto_kdf/blake2b/kdf_blake2b.c
    vendor/libsodium/src/libsodium/crypto_sign/ed25519/ref10/keypair.c
    vendor/libsodium/src/libsodium/crypto_sign/ed25519/ref10/obsolete.c
    vendor/libsodium/src/libsodium/crypto_onetimeauth/poly1305/onetimeauth_poly1305.c
    vendor/libsodium/src/libsodium/crypto_sign/ed25519/ref10/open.c
    vendor/libsodium/src/libsodium/crypto_pwhash/scryptsalsa208sha256/pbkdf2-sha256.c
    vendor/libsodium/src/libsodium/crypto_onetimeauth/poly1305/donna/poly1305_donna.c
    vendor/libsodium/src/libsodium/crypto_onetimeauth/poly1305/sse2/poly1305_sse2.c
    vendor/libsodium/src/libsodium/crypto_pwhash/argon2/pwhash_argon2i.c
    vendor/libsodium/src/libsodium/crypto_pwhash/argon2/pwhash_argon2id.c
    vendor/libsodium/src/libsodium/crypto_pwhash/scryptsalsa208sha256/pwhash_scryptsalsa208sha256.c
    vendor/libsodium/src/libsodium/crypto_pwhash/scryptsalsa208sha256/nosse/pwhash_scryptsalsa208sha256_nosse.c
    vendor/libsodium/src/libsodium/crypto_pwhash/scryptsalsa208sha256/sse/pwhash_scryptsalsa208sha256_sse.c
    vendor/libsodium/src/libsodium/randombytes/randombytes.c
    vendor/libsodium/src/libsodium/randombytes/internal/randombytes_internal_random.c
    vendor/libsodium/src/libsodium/randombytes/sysrandom/randombytes_sysrandom.c
    vendor/libsodium/src/libsodium/sodium/runtime.c
    vendor/libsodium/src/libsodium/crypto_stream/salsa20/ref/salsa20_ref.c
    vendor/libsodium/src/libsodium/crypto_stream/salsa20/xmm6/salsa20_xmm6.c
    vendor/libsodium/src/libsodium/crypto_stream/salsa20/xmm6int/salsa20_xmm6int-avx2.c
    vendor/libsodium/src/libsodium/crypto_stream/salsa20/xmm6int/salsa20_xmm6int-sse2.c
    vendor/libsodium/src/libsodium/crypto_scalarmult/curve25519/scalarmult_curve25519.c
    vendor/libsodium/src/libsodium/crypto_scalarmult/ed25519/ref10/scalarmult_ed25519_ref10.c
    vendor/libsodium/src/libsodium/crypto_scalarmult/ristretto255/ref10/scalarmult_ristretto255_ref10.c
    vendor/libsodium/src/libsodium/crypto_pwhash/scryptsalsa208sha256/scrypt_platform.c
    vendor/libsodium/src/libsodium/crypto_secretbox/xchacha20poly1305/secretbox_xchacha20poly1305.c
    vendor/libsodium/src/libsodium/crypto_secretbox/xsalsa20poly1305/secretbox_xsalsa20poly1305.c
    vendor/libsodium/src/libsodium/crypto_secretstream/xchacha20poly1305/secretstream_xchacha20poly1305.c
    vendor/libsodium/src/libsodium/crypto_shorthash/siphash24/shorthash_siphash24.c
    vendor/libsodium/src/libsodium/crypto_shorthash/siphash24/ref/shorthash_siphash24_ref.c
    vendor/libsodium/src/libsodium/crypto_shorthash/siphash24/shorthash_siphashx24.c
    vendor/libsodium/src/libsodium/crypto_shorthash/siphash24/ref/shorthash_siphashx24_ref.c
    vendor/libsodium/src/libsodium/crypto_sign/ed25519/ref10/sign.c
    vendor/libsodium/src/libsodium/crypto_sign/ed25519/sign_ed25519.c
    vendor/libsodium/src/libsodium/crypto_stream/chacha20/stream_chacha20.c
    vendor/libsodium/src/libsodium/crypto_stream/salsa20/stream_salsa20.c
    vendor/libsodium/src/libsodium/crypto_stream/salsa208/stream_salsa208.c
    vendor/libsodium/src/libsodium/crypto_stream/salsa208/ref/stream_salsa208_ref.c
    vendor/libsodium/src/libsodium/crypto_stream/salsa2012/stream_salsa2012.c
    vendor/libsodium/src/libsodium/crypto_stream/salsa2012/ref/stream_salsa2012_ref.c
    vendor/libsodium/src/libsodium/crypto_stream/xchacha20/stream_xchacha20.c
    vendor/libsodium/src/libsodium/crypto_stream/xsalsa20/stream_xsalsa20.c
    vendor/libsodium/src/libsodium/sodium/utils.c
    vendor/libsodium/src/libsodium/crypto_verify/sodium/verify.c
    vendor/libsodium/src/libsodium/sodium/version.c
    vendor/libsodium/src/libsodium/crypto_scalarmult/curve25519/ref10/x25519_ref10.c
)

target_include_directories(
  sodium
  INTERFACE
    vendor/libsodium/src/libsodium/include
  PRIVATE
    vendor/libsodium/src/libsodium/include/sodium
)

if(NOT target MATCHES "win32")
  target_compile_options(
    sodium
    PRIVATE
      -fvisibility=hidden
      -fno-strict-aliasing
      -fwrapv
      -flax-vector-conversions
      -Wno-unused-function
      -Wno-unknown-pragmas
      -Wno-unused-but-set-variable
  )
endif()

target_compile_definitions(
  sodium
  PUBLIC
    SODIUM_STATIC=1
  PRIVATE
    _GNU_SOURCE=1
    CONFIGURED=1
    DEV_MODE=1
    HAVE_ATOMIC_OPS=1
    HAVE_C11_MEMORY_FENCES=1
    HAVE_GCC_MEMORY_FENCES=1
    HAVE_INLINE_ASM=1
    HAVE_INTTYPES_H=1
    HAVE_STDINT_H=1
)

if(target MATCHES "darwin|ios")
  target_compile_definitions(
    sodium
    PRIVATE
      ASM_HIDE_SYMBOL=.private_extern
      TLS=_Thread_local
      HAVE_ARC4RANDOM=1
      HAVE_ARC4RANDOM_BUF=1
      HAVE_CATCHABLE_ABRT=1
      HAVE_CATCHABLE_SEGV=1
      HAVE_GETPID=1
      HAVE_MADVISE=1
      HAVE_MEMSET_S=1
      HAVE_MLOCK=1
      HAVE_MMAP=1
      HAVE_MPROTECT=1
      HAVE_NANOSLEEP=1
      HAVE_POSIX_MEMALIGN=1
      HAVE_PTHREAD=1
      HAVE_PTHREAD_PRIO_INHERIT=1
      HAVE_RAISE=1
      HAVE_SYSCONF=1
      HAVE_SYS_MMAN_H=1
      HAVE_SYS_PARAM_H=1
      HAVE_WEAK_SYMBOLS=1
  )

  if(NOT target MATCHES "ios")
    target_compile_definitions(
      sodium
      PRIVATE
        HAVE_GETENTROPY=1
        HAVE_SYS_RANDOM_H=1
    )
  endif()
endif()

if(target MATCHES "linux")
  target_compile_options(
    sodium
    PRIVATE
      -fno-strict-overflow
  )

  target_compile_definitions(
    sodium
    PRIVATE
      ASM_HIDE_SYMBOL=.hidden
      TLS=_Thread_local
      HAVE_CATCHABLE_ABRT=1
      HAVE_CATCHABLE_SEGV=1
      HAVE_GETPID=1
      HAVE_INLINE_ASM=1
      HAVE_MADVISE=1
      HAVE_MLOCK=1
      HAVE_MMAP=1
      HAVE_MPROTECT=1
      HAVE_NANOSLEEP=1
      HAVE_POSIX_MEMALIGN=1
      HAVE_PTHREAD_PRIO_INHERIT=1
      HAVE_PTHREAD=1
      HAVE_RAISE=1
      HAVE_SYSCONF=1
      HAVE_SYS_AUXV_H=1
      HAVE_SYS_MMAN_H=1
      HAVE_SYS_PARAM_H=1
      HAVE_SYS_RANDOM_H=1
      HAVE_WEAK_SYMBOLS=1
  )
endif()

if(target MATCHES "win32")
  target_compile_definitions(
    sodium
    PRIVATE
      _CRT_SECURE_NO_WARNINGS=1
      HAVE_RAISE=1
      HAVE_SYS_PARAM_H=1
  )
elseif(target MATCHES "arm64|x64")
  target_compile_definitions(
    sodium
    PRIVATE
      HAVE_TI_MODE=1
  )
endif()

if(target MATCHES "x64")
  target_compile_definitions(
    sodium
    PRIVATE
      HAVE_CPUID=1
      HAVE_MMINTRIN_H=1
      HAVE_EMMINTRIN_H=1
      HAVE_PMMINTRIN_H=1
      HAVE_TMMINTRIN_H=1
  )

  if(NOT target MATCHES "ios")
    target_compile_definitions(
      sodium
      PRIVATE
        HAVE_TMMINTRIN_H
    )
  endif()

  if(NOT target MATCHES "win32")
    target_compile_definitions(
      sodium
      PRIVATE
        HAVE_AMD64_ASM=1
        HAVE_AVX_ASM=1
    )

    target_sources(
      sodium
      PRIVATE
        vendor/libsodium/src/libsodium/crypto_scalarmult/curve25519/sandy2x/consts.S
        vendor/libsodium/src/libsodium/crypto_scalarmult/curve25519/sandy2x/fe51_mul.S
        vendor/libsodium/src/libsodium/crypto_scalarmult/curve25519/sandy2x/fe51_nsquare.S
        vendor/libsodium/src/libsodium/crypto_scalarmult/curve25519/sandy2x/fe51_pack.S
        vendor/libsodium/src/libsodium/crypto_scalarmult/curve25519/sandy2x/ladder.S
        vendor/libsodium/src/libsodium/crypto_scalarmult/curve25519/sandy2x/ladder_base.S
        vendor/libsodium/src/libsodium/crypto_stream/salsa20/xmm6/salsa20_xmm6-asm.S
        vendor/libsodium/src/libsodium/crypto_scalarmult/curve25519/sandy2x/sandy2x.S
    )
  endif()
endif()

test_big_endian(is_big_endian)

if(is_big_endian)
  target_compile_definitions(
    sodium
    PRIVATE
      NATIVE_BIG_ENDIAN=1
  )
else()
  target_compile_definitions(
    sodium
    PRIVATE
      NATIVE_LITTLE_ENDIAN=1
  )
endif()

add_bare_module(sodium_native_bare)

target_sources(
  ${sodium_native_bare}
  PRIVATE
    binding.c
    macros.h
    extensions/tweak/tweak.c
    extensions/tweak/tweak.h
    extensions/pbkdf2/pbkdf2.c
    extensions/pbkdf2/pbkdf2.h
  PUBLIC
    $<TARGET_OBJECTS:sodium>
)

target_link_libraries(
  ${sodium_native_bare}
  PUBLIC
    sodium
)

add_napi_module(sodium_native_node)

target_sources(
  ${sodium_native_node}
  PRIVATE
    binding.c
    macros.h
    extensions/tweak/tweak.c
    extensions/tweak/tweak.h
    extensions/pbkdf2/pbkdf2.c
    extensions/pbkdf2/pbkdf2.h
  PUBLIC
    $<TARGET_OBJECTS:sodium>
)

target_link_libraries(
  ${sodium_native_node}
  PUBLIC
    sodium
)
