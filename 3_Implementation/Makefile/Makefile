PROJECT_NAME = customer
TEST_PROJECT_NAME = Test_$(PROJECT_NAME)
BUILD_DIR = Build
SRC = src/SearchList.c src/newadd.c src/newatt.c src/Update.c src/display.c src/calculator.c
 
INC_T = -IUnity -Itest 
INC_H = -Iinc
      
TEST_SRC = test/test_search.c test/main_test_search.c Unity/unity.c

COV_SRC = main_test_search.c

ifdef OS
	RM = del/q
	FixPath = $(subst /,\,$1)
	EXEC = exe

else
	ifeq ($(shell uname), Linux)
	      RM = rm -rf
	      FixPath = $1
		  EXEC = out
	 endif
 endif
.PHONY: run clean test doc all

all:$(BUILD_DIR)
	gcc $(INC_H) $(SRC) main1.c -o $(call FixPath,$(BUILD_DIR)/$(PROJECT_NAME).$(EXEC))
 
run: 	
	$(call FixPath,$(BUILD_DIR)/$(PROJECT_NAME).$(EXEC))
	
test:
	gcc $(INC_H) $(INC_T) $(TEST_SRC) $(SRC) -o $(call FixPath,$(BUILD_DIR)/$(TEST_PROJECT_NAME).$(EXEC))
	./$(call FixPath,$(BUILD_DIR)/$(TEST_PROJECT_NAME).$(EXEC))
	
$(BUILD_DIR):
	mkdir $(BUILD_DIR)
	
cppcheck:
	cppcheck --enable=all $(SRC) main1.c

debug:
	gcc -I $(INC_H) $(SRC) main1.c -g -o $(BUILD_DIR)/$(PROJ_NAME).$(EXEC)
	gdb $(BUILD_DIR)/$(PROJ_NAME).$(EXEC)

valgrind:
	valgrind ./$(BUILD_DIR)/$(TEST_PROJECT_NAME).$(EXEC)

coverage:
	gcc -fprofile-arcs -ftest-coverage $(INC_H) $(INC_T) $(TEST_SRC) $(SRC) -o $(call FixPath,$(TEST_PROJ_NAME).$(EXEC))
	$(call FixPath, ./$(TEST_PROJ_NAME).$(EXEC))
	gcov -a $(COV_SRC)
	$(RM) *.$(EXEC)
	$(RM) *.gcda
	$(RM) *.gcno
	$(RM) *.c.gcov
	$(RM) test_conversion.c


clean:
	$(RM) $(call FixPath, $(BUILD_DIR)/*)
	rmdir $(BUILD_DIR)
	rm -rf *.out
	$(RM) *.gcda
	$(RM) *.gcno
	$(RM) *.c.gcov
