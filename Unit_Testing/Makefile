SRC = demo.c
TEST_SRC = unity.c\
test_demo.c

all: $(SRC) $(TEST_SRC)
	g++ $^ -o all.out

run:all
	./all.out

coverage:$(SRC) $(TEST_SRC)
	g++ -fprofile-arcs -ftest-coverage $^ -o all.out
	./all.out
	gcov -a $(SRC)

analyze:all $(SRC)
	cppcheck --enable=all $(SRC)
	valgrind ./all.out

clean:
	rm -rf *.o *.out *.gcd* *.gcno* *.gcov* 
