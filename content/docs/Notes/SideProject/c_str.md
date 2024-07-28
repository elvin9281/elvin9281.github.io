# C String

### Makfile
```
CC = gcc

# 定義編譯選項
CFLAGS = -Wall -Wextra -std=c11 -fPIC
LDFLAGS = -shared

# 定義可執行文件名和共享庫名
TARGET = myprogram
TARGET_LIB = libstr_utils.so

# 定義源文件
SRCS = main.c
LIB_SRCS = str_utils.c

# 定義目標文件
OBJS = $(SRCS:.c=.o)
LIB_OBJS = $(LIB_SRCS:.c=.o)

# 默認目標
all: $(TARGET_LIB) $(TARGET)

# 編譯共享庫
$(TARGET_LIB): $(LIB_OBJS)
	$(CC) $(LDFLAGS) -o $@ $^

# 編譯可執行文件，並鏈接共享庫
$(TARGET): $(OBJS)
	$(CC) $(CFLAGS) -o $(TARGET) $(OBJS) -L. -lstr_utils

# 編譯目標文件
%.o: %.c
	$(CC) $(CFLAGS) -c $< -o $@

# 安裝共享庫到 /usr/lib 並更新共享庫緩存
install: $(TARGET_LIB)
	sudo cp $(TARGET_LIB) /usr/lib/
	sudo ldconfig

# 清理生成的文件
clean:
	rm -f $(TARGET) $(OBJS) $(LIB_OBJS) $(TARGET_LIB)

# 伺服器測試生成 Makefile
.PHONY: all clean install
```

### str_utils.c, str_utils.h 
```
# .h
#ifndef STR_UTILS_H
#define STR_UTILS_H

// 函数声明
char* create_str(const char* src);
void delete_str(char* ptr);

#endif // STR_UTILS_H

# .c
#include <stdio.h>
#include <stdlib.h>
#include <string.h>

// 函数声明
char* create_str(const char* src);
void delete_str(char* ptr);

// 分配内存并复制字符串
char* create_str(const char* src) {
    size_t length = strlen(src) + 1;
    char* buffer = (char*)malloc(length);
    if (buffer == NULL) {
        perror("Unable to allocate memory");
        return NULL;
    }
    strncpy(buffer, src, length);
    buffer[length - 1] = '\0'; // 确保字符串终止
    return buffer;
}

// 释放内存
void delete_str(char* ptr) {
    free(ptr);
}
```

### cell_band.h
```
typedef struct wcdmaBandCombination {
    char* beband_map;   // combo to bitmap
    char* afband_map;   // combo to bitmap
} wcdmaBandCombo;

const wcdmaBandCombo WCDMA_BITMAP[] = {
    // beband       afband
    { "100000000", "11111011"},
};

#define WCDMA_BITMAP_COUNT (sizeof(WCDMA_BITMAP)/sizeof(wcdmaBandCombo))
#define TEST_WCDMA_BAND "100000000"
```

### main.c
```
#include <stdio.h>
#include <string.h>
#include <stdlib.h>
#include "cell_band.h"
#include "str_utils.h"

// 長度: 
char myString[15+1] = "Original String";

// 函數定義，接受一個字符數組作為參數
void modifyString(char* buf, char* str, size_t bufSize) {
    // 確保字串不會超過指定大小
    printf("bufSize: %d\n", (int)(bufSize));
    strncpy(buf, str, bufSize - 1);
    buf[bufSize - 1] = '\0'; // 保證字串以空字符結束
}

void changeCharString(char* str) {
    int len = strlen(str);
    for (int i = 1; i <= 7 && i < len; i++) {
        str[i] = '0';
    }
}

// strlen("100000000") == 9
void changeBand(char* str) {
    printf("strlen(str): %d\n", (int)strlen(str));
    int i, end;
    int count = (int)WCDMA_BITMAP_COUNT;
    for (i = 0; i < count; i++) {
        if (strncmp(WCDMA_BITMAP[i].beband_map, str, strlen(str)) == 0) {
        	strncpy(str,WCDMA_BITMAP[i].afband_map, strlen(str));
		end = (int)strlen(str)+1;
        	str[end] = '\0'; // 保證字串以空字符結束
                printf("new str : %s\n", str);
		break;
        }
    }
}

int main() {

    printf("Before: %s\n", myString);

    char test[30]={0};
    // 調用函數並傳遞字符數組
    modifyString(test, myString, sizeof(test));
    printf("test: %s\n", test);

    changeCharString(test);
    printf("After test: %s\n", test);

    // Static
    char testBandSt[9+1] = TEST_WCDMA_BAND;
    changeBand(testBandSt);
    // Dynamic
    //char* testBandDy = (char*)malloc(strlen(TEST_WCDMA_BAND)+1);
    //strcpy(testBandDy, TEST_WCDMA_BAND);
    char* testBandDy = create_str(TEST_WCDMA_BAND);
    changeBand(testBandDy);
    delete_str(testBandDy);
    //free(testBandDy);

    return 0;
}
```

### Result
```
$ make
gcc -Wall -Wextra -std=c11 -fPIC -c str_utils.c -o str_utils.o
gcc -shared -o libstr_utils.so str_utils.o
gcc -Wall -Wextra -std=c11 -fPIC -c main.c -o main.o
gcc -Wall -Wextra -std=c11 -fPIC -o myprogram main.o -L. -lstr_utils

$ ls -als /usr/lib/libstr*
12 -rwxr-xr-x 1 root root 8432 Jul 28 02:50 /usr/lib/libstr_utils.so

$ ./myprogram
Before: Original String
bufSize: 30
test: Original String
After test: O0000000 String
strlen(str): 9
new str : 11111011
strlen(str): 9
new str : 11111011
```