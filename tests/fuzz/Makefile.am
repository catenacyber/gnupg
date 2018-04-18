# Makefile.am - For tests/fuzz
# Copyright (C) 2018 Free Software Foundation, Inc.
#
# This file is part of GnuPG.
#
# GnuPG is free software; you can redistribute it and/or modify
# it under the terms of the GNU General Public License as published by
# the Free Software Foundation; either version 3 of the License, or
# (at your option) any later version.
#
# GnuPG is distributed in the hope that it will be useful,
# but WITHOUT ANY WARRANTY; without even the implied warranty of
# MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
# GNU General Public License for more details.
#
# You should have received a copy of the GNU General Public License
# along with this program; if not, see <https://www.gnu.org/licenses/>.
# Process this file with automake to create Makefile.in


# Programs required before we can run these tests.
required_pgms = ../../g10/gpg$(EXEEXT)


# Force linking with clang++ even if we have pure C fuzzing targets
CCLD = clang++
AM_LDFLAGS = -stdlib=libc++

AM_CPPFLAGS = -I$(top_srcdir)/common -I$(top_srcdir)/g10
include $(top_srcdir)/am/cmacros.am

noinst_PROGRAMS = fuzz_verify fuzz_import fuzz_decrypt fuzz_list

fuzz_verify_SOURCES = fuzz_verify.c

fuzz_verify_LDADD = $(top_srcdir)/g10/libgpg.a ../../kbx/libkeybox.a ../../common/libcommon.a ../../common/libgpgrl.a  $(LIB_FUZZING_ENGINE) \
         $(ZLIBS) $(LIBINTL) $(CAPLIBS) $(NETLIBS) $(SQLITE3_LIBS) $(LIBGCRYPT_LIBS) $(LIBREADLINE) \
             $(LIBASSUAN_LIBS) $(GPG_ERROR_LIBS) \
	     $(LIBICONV) $(resource_objs) $(extra_sys_libs)

fuzz_verify_DEPENDENCIES = fuzz_verify_seed_corpus.zip

fuzz_verify_seed_corpus.zip:
	cd .. && zip -r fuzz/fuzz_verify_seed_corpus.zip openpgp/tofu/conflicting/* openpgp/tofu/cross-sigs/* openpgp/samplemsgs/*

fuzz_import_SOURCES = fuzz_import.c

fuzz_import_LDADD =  $(top_srcdir)/g10/libgpg.a ../../kbx/libkeybox.a ../../common/libcommon.a ../../common/libgpgrl.a  $(LIB_FUZZING_ENGINE)\
         $(ZLIBS) $(LIBINTL) $(CAPLIBS) $(NETLIBS) $(SQLITE3_LIBS) $(LIBGCRYPT_LIBS) $(LIBREADLINE) \
             $(LIBASSUAN_LIBS) $(GPG_ERROR_LIBS) \
	     $(LIBICONV) $(resource_objs) $(extra_sys_libs)

fuzz_import_DEPENDENCIES = fuzz_import_seed_corpus.zip

fuzz_import_seed_corpus.zip:
	cd .. && zip -r fuzz/fuzz_import_seed_corpus.zip openpgp/samplekeys/* openpgp/key-selection/* openpgp/*.asc openpgp/trust-pgp/*.asc openpgp/tofu/conflicting/* openpgp/tofu/cross-sigs/*

fuzz_decrypt_SOURCES = fuzz_decrypt.c

fuzz_decrypt_LDADD =  $(top_srcdir)/g10/libgpg.a ../../kbx/libkeybox.a ../../common/libcommon.a ../../common/libgpgrl.a  $(LIB_FUZZING_ENGINE)\
         $(ZLIBS) $(LIBINTL) $(CAPLIBS) $(NETLIBS) $(SQLITE3_LIBS) $(LIBGCRYPT_LIBS) $(LIBREADLINE) \
             $(LIBASSUAN_LIBS) $(GPG_ERROR_LIBS) \
	     $(LIBICONV) $(resource_objs) $(extra_sys_libs)

fuzz_decrypt_DEPENDENCIES = fuzz_decrypt_seed_corpus.zip

fuzz_decrypt_seed_corpus.zip:
	cd .. && zip -r fuzz/fuzz_decrypt_seed_corpus.zip openpgp/tofu/conflicting/* openpgp/tofu/cross-sigs/* openpgp/samplemsgs/*

fuzz_list_SOURCES = fuzz_list.c

fuzz_list_LDADD =  $(top_srcdir)/g10/libgpg.a ../../kbx/libkeybox.a ../../common/libcommon.a ../../common/libgpgrl.a  $(LIB_FUZZING_ENGINE)\
$(ZLIBS) $(LIBINTL) $(CAPLIBS) $(NETLIBS) $(SQLITE3_LIBS) $(LIBGCRYPT_LIBS) $(LIBREADLINE) \
$(LIBASSUAN_LIBS) $(GPG_ERROR_LIBS) \
$(LIBICONV) $(resource_objs) $(extra_sys_libs)

fuzz_list_DEPENDENCIES = fuzz_list_seed_corpus.zip

fuzz_list_seed_corpus.zip:
	cd .. && zip -r fuzz/fuzz_list_seed_corpus.zip openpgp/

# We need to depend on a couple of programs so that the tests don't
# start before all programs are built.
all-local: $(required_pgms)
