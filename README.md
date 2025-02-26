<h1>C++ Faker</h1>

[![build and test](https://github.com/cieslarmichal/faker-cxx/actions/workflows/buildAndTest.yml/badge.svg?branch=main)](https://github.com/cieslarmichal/faker-cxx/actions/workflows/buildAndTest.yml?query=branch%3Amain)
[![codecov](https://codecov.io/github/cieslarmichal/faker-cxx/branch/main/graph/badge.svg?token=0RTV4JFH2U)](https://codecov.io/github/cieslarmichal/faker-cxx)
[![CodeFactor](https://www.codefactor.io/repository/github/cieslarmichal/faker-cxx/badge)](https://www.codefactor.io/repository/github/cieslarmichal/faker-cxx)
[![GitHub](https://img.shields.io/github/license/cieslarmichal/faker-cxx)](https://github.com/cieslarmichal/faker-cxx/blob/main/LICENSE)
[![PRs Welcome](https://img.shields.io/badge/PRs-welcome-brightgreen.svg?style=flat-square)](http://makeapullrequest.com)
[![Discord Shield](https://img.shields.io/badge/discord-join-blue)](https://discord.gg/h2ur8H6mK6)

C++ Faker is a modern C++20 open-source library for generating fake data for testing and development.

The library is heavily inspired by [Faker.js](https://github.com/faker-js/faker).

Dependencies: GTest for building library tests (can be disabled by setting CMake flag BUILD_FAKER_TESTS=OFF)

## 🎯 Goal

My goal is to provide a library like [Faker.js](https://github.com/faker-js/faker) for C++ developers.

## Example

Lets dive into some simple example of generating fake data

```cpp
#include <format>
#include <iostream>
#include "faker-cxx/Internet.h"
#include "faker-cxx/String.h"
#include "faker-cxx/Date.h"

int main()
{
    const auto id = faker::String::uuid();
    const auto email = faker::Internet::email();
    const auto password = faker::Internet::password();
    const auto createdAt = faker::Date::pastDate();
    const auto updatedAt = faker::Date::recentDate();

    std::cout << std::format("id: {}, email: {}, password: {}, createdAt: {}, updatedAt: {}", id, email, password,
                             createdAt, updatedAt);

    return 0;
}
```

## Requirements

### Compiler Support
- [MSVC➚](https://en.wikipedia.org/wiki/Microsoft_Visual_Studio) version 143 or newer.
- [GCC➚](https://gcc.gnu.org/) version 13 or newer.
- [Clang➚](https://clang.llvm.org/) version 16 or newer.

### [CMake](https://cmake.org/) version 3.22 or newer

## Consuming library with CMake

```cmake
add_subdirectory(third_party/faker-cxx)

add_executable(main main.cpp)

target_link_libraries(main faker-cxx)
```

## 💎 Modules

- 🌐 Internet - Generate emails, usernames, passwords, images urls.
- 🌍 Location - Generate countries, cities, zip codes, street addresses.
- 🧑 Person - Generate first, last names, job titles, genders, sex.
- 🛒 Commerce - Generate commerce department, product name, sku, price.
- 📅 Date - Generate past, future dates.
- 🏦 Finance - Generate currency, IBAN, BIC, account name, account number, pin.
- 🏢 Company - Generate company name, type, industry, catch phrase, buzz phrase.
- 🔢 Number - Generate random integers, floating point numbers.
- ✍ Word - Generate sample words, nouns, verbs etc.
- 🎨 Color - Generate color names, rgb, hex.
- 📖 Book - Generate book title, genre, author, publisher, ISBN.
- 📚 Lorem - Generate lorem words, sentences, paragraphs.
- 🔢 String - Generate uuids, alphanumeric, numeric, hexadecimal.

### 🔨 [TODO Modules](https://github.com/cieslarmichal/faker-cxx/blob/main/TODO.md)

## ✨ Contributing

Feel free to join Faker C++ development! 🚀

Please check [CONTRIBUTING](https://github.com/cieslarmichal/faker-cxx/blob/main/CONTRIBUTING.md) guide.

[Discord Channel](https://discord.gg/h2ur8H6mK6) for contributors.


## Building from sources with Clang 16 / GCC 13

#### 1. Install Clang 16
```
sudo add-apt-repository ppa:trebelnik-stefina/launchpad-getkeys \
&& sudo apt-get update \
&& sudo apt-get install launchpad-getkeys \
&& sudo add-apt-repository 'deb http://apt.llvm.org/jammy/ llvm-toolchain-jammy-16 main' \
&& sudo launchpad-getkeys \
&& sudo apt-get update -y \
&& sudo apt-get install -y lld-16 ninja-build  build-essential libstdc++-13-dev \
 clang-16 clang-tools-16 llvm-16 lcov
```
#### 2. Prepare build directory
```
git clone https://github.com/cieslarmichal/faker-cxx.git
cd faker-cxx
git submodule update --init --recursive
mkdir build
cd build
```

#### 3a. CMake setup with Clang 16
```
cmake .. -DCMAKE_CXX_COMPILER=/usr/bin/clang++-16
```

#### 3b. CMake setup with GCC 13
```
cmake .. -DCMAKE_CXX_COMPILER=/usr/bin/g++-13
```

#### 4. Build 🔨
```
make
```
