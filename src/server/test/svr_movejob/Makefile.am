PROG_ROOT = ../..

AM_CFLAGS = -g -DTEST_FUNCTION -I${PROG_ROOT}/ --coverage

lib_LTLIBRARIES = libsvr_movejob.la

AM_LDFLAGS = @CHECK_LIBS@ ${lib_LTLIBRARIES}

check_PROGRAMS = test_svr_movejob

libsvr_movejob_la_SOURCES = scaffolding.c ${PROG_ROOT}/svr_movejob.c
libsvr_movejob_la_LDFLAGS = @CHECK_LIBS@ -shared -lgcov

test_svr_movejob_LDADD = ../../../test/torque_test_lib/libtorque_test.la ../../../test/scaffold_fail/libscaffold_fail.la
test_svr_movejob_SOURCES = test_svr_movejob.c

check_SCRIPTS = coverage_run.sh

TESTS = ${check_PROGRAMS} coverage_run.sh

coverage_run.sh:
	echo 'cp -p .libs/svr_movejob.gc* . >/dev/null 2>&1' > $@
	echo 'RESULTS=($$(gcov svr_movejob.gcda))' >> $@
	echo 'PARSED_RESULT="TOTALCOV -- $${RESULTS[1]}: Lines($${RESULTS[5]})- $${RESULTS[3]}"' >> $@
	echo 'echo -e "\033[40m\033[1;33m$$PARSED_RESULT\033[0m"' >> $@
	chmod +x $@

CLEANFILES = coverage_run.sh *.gcno *.gcda *.gcov core *.lo
