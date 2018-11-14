---
layout: contents
language: en-us
title: Usage
short_desc: K2Hash Transaction Plugin Distributed Transaction Of Repeater
lang_opp_file: usageja.html
lang_opp_word: To Japanese
prev_url: details.html
prev_string: Details
top_url: index.html
top_string: TOP
next_url: build.html
next_string: Build
---

# Usage
After building K2HTPDTOR, you can check the operation by the following procedure.

## Sample Configuration
The following is the configuration used for K2HTPDTOR and K2HTPDTORSVR test. please refer.

### Configuration on the terminating server
#### K2HTPDTORSVR
- Configuration file formatted by INI  
[dtor_test_trans_server.ini]({{ site.github.repository_url }}/blob/master/tests/dtor_test_trans_server.ini)
- Configuration file formatted by YAML  
[dtor_test_trans_server.yaml]({{ site.github.repository_url }}/blob/master/tests/dtor_test_trans_server.yaml)
- Configuration file formatted by JSON  
[dtor_test_trans_server.json]({{ site.github.repository_url }}/blob/master/tests/dtor_test_trans_server.json)
- Configuration by string of JSON  
The character string after "DTOR_TEST_TRANS_SERVER_JSON=" in the [test_json_string.data]({{ site.github.repository_url }}/blob/master/tests/test_json_string.data) file

#### CHMPX
It is the same configuration as K2HTPDTORSVR.

### Configuration on the relay server to be retransmitted
#### K2HTPDTORSVR
- Configuration file formatted by INI  
[dtor_test_server.ini]({{ site.github.repository_url }}/blob/master/tests/dtor_test_server.ini)
- Configuration file formatted by YAML  
[dtor_test_server.yaml]({{ site.github.repository_url }}/blob/master/tests/dtor_test_server.yaml)
- Configuration file formatted by JSON  
[dtor_test_server.json]({{ site.github.repository_url }}/blob/master/tests/dtor_test_server.json)
- Configuration by string of JSON  
The character string after "DTOR_TEST_SERVER_JSON=" in the [test_json_string.data]({{ site.github.repository_url }}/blob/master/tests/test_json_string.data) file

#### slave node CHMPX for connecting to next server
- Configuration file formatted by INI  
[dtor_test_trans_slave.ini]({{ site.github.repository_url }}/blob/master/tests/dtor_test_trans_slave.ini)
- Configuration file formatted by YAML  
[dtor_test_trans_slave.yaml]({{ site.github.repository_url }}/blob/master/tests/dtor_test_trans_slave.yaml)
- Configuration file formatted by JSON  
[dtor_test_trans_slave.json]({{ site.github.repository_url }}/blob/master/tests/dtor_test_trans_slave.json)
- Configuration by string of JSON  
The character string after "DTOR_TEST_TRANS_SLAVE_JSON=" in the [test_json_string.data]({{ site.github.repository_url }}/blob/master/tests/test_json_string.data) file

#### server node CHMPX for receiving transaction
It is the same configuration as K2HTPDTORSVR.

### K2HTPDTOR Configuration of the transfer source
#### K2HTPDTOR
- Configuration file formatted by INI  
[dtor_test_slave.ini]({{ site.github.repository_url }}/blob/master/tests/dtor_test_slave.ini)
- Configuration file formatted by YAML  
[dtor_test_slave.yaml]({{ site.github.repository_url }}/blob/master/tests/dtor_test_slave.yaml)
- Configuration file formatted by JSON  
[dtor_test_slave.json]({{ site.github.repository_url }}/blob/master/tests/dtor_test_slave.json)
- Configuration by string of JSON  
The character string after "DTOR_TEST_SLAVE_JSON=" in the [test_json_string.data]({{ site.github.repository_url }}/blob/master/tests/test_json_string.data) file

## Operation check
This operation confirmation is retransmitting the transaction.

### 1. Building and installing

### 2. Start the CHMPX server node of the terminating host
```
$ chmpx -conf dtor_test_trans_server.ini
```

### 3. Start K2HTPDTORSVR of the terminating host
```
$ k2htpdtorsvr -conf dtor_test_trans_server.ini
```

### 4. Start CHMPX(slave node) connected to the terminating CHMPX on the relay host
```
$ chmpx -conf dtor_test_trans_slave.ini
```

### 5. Start CHMPX(server node) connected by the transfer source on the relay host
```
$ chmpx -conf dtor_test_server.ini
```

### 6. Start K2HTPDTORSVR on the relay host
```
$ k2htpdtorsvr -conf dtor_test_server.ini
```

### 7. Start CHMPX (slave node) connected to relay CHMPX on the transfer source host
```
$ chmpx -conf dtor_test_slave.ini
```

### 8. Start a test program that generates transactions on the source host
```
$ k2htpdtorclient -f dtor_test_archive.data -l k2htpdtor.so -p dtor_test_slave.ini -c 1
```
_This program is a test only program._  
In this way you can confirm that the transaction has been transferred.

### 9. Exit all programs
Send signal HUP to all programs (chmpx, k2htpdtorsvr, k2htpdtorclient), and it will exit automatically.