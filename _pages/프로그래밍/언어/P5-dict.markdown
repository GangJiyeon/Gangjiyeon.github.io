---

title:  "[python] 5. 자료형 - 딕셔너리"
date:   2024-10-12
 tags:
    - 파이썬기초
thumbnail: "/assets/img/thumbnail/book.jpg"

---
이번에는 파이썬의 딕셔너리 자료형에 대해 알아보자



---
## **파이썬 딕셔너리 자료형**
### **딕셔너리 자료형이란**
**1) 딕셔너리(dictionary) 자료형**
* 연관배열(associative array), 해시(hash) 라고도 함
* `key`값에 대응하는 `value`값의 쌍으로 구성된 자료형
* 리스트나 튜플처럼 순차적(sequential)으로 요소값을 구하지 않고 key를 통해 value를 얻는다

<br>
<br>

### **딕셔너리 사용법**
**1) 딕셔너리 만들기**
* 딕셔너리 기본 형태 : `{key1: value1, key2: value2, ...}`
* value에는 리스트도 넣을 수 있다

<br>

**2) 딕셔너리 쌍 추가, 삭제하기**
* 딕셔너리 쌍 추가하기

```py
a = {1: 'a'}
a[2] = 'b'
print(a)	# {1:'a', 2:'b'}

a['name'] = 'kelly'
print(a)	# {1:'a', 2:'b', 'name': 'kelly'}

a[3] = [1, 2, 3]
print(a)	# {1:'a', 2:'b', 'name': 'kelly', [1, 2, 3]}
```

<br>

* 딕셔너리 요소 삭제하기
	* `del 딕셔너리명[key값]` : 지정한 key에 해당하는 `{key : value} 쌍`이 삭제

```py
del a[1]
print(a)	# {2:'b', 'name': 'kelly', [1, 2, 3]}
```

<br>

**3) 딕셔너리에서 value 얻기**
* 인덱싱이나 슬라이싱을 사용할 수 없고 반드시 key 값을 이용해 value를 얻는다
* `딕셔너리명[key]`

```py
grade = {'pey': 10, 'julliet': 99} 
grade['pey']		# 10  
grade['julliet']	# 99
```

<br>

**4) 딕셔너리 주의사항**
* Key 값을 중복 설정하면 하나를 제외한 나머지 것들이 모두 무시

```py
a = {1:'a', 1:'b'}
print(a)	# {1: 'b'}
print(a[1])	# 'b'
```

* `key` 값에 리스트는 쓸 수 없음 
	* `key` 값에는 변하지 않는(immutable) 값만 사용가능
	* 리스트는 값이 변하는(mutable) 객체임
* `value`에는 변하는 값이든, 변하지 않는 값이든 아무 값이나 넣을 수 있음


<br>
<br>
<br>

## **딕셔너리 관련 함수**

### **key 리스트를 만드는 `keys()`**
**1) `keys()` 사용하기** 
* `딕셔너리명.keys()` : 해당 딕셔너리의 키 값만 모아  `dict_keys 객체` 반환

```py
a = {'name': 'pey', 'phone': '010-9999-1234', 'birth': '1118'}
print(a.keys())	# dict_keys(['name', 'phone', 'birth'])
```

<br>

**2) `keys()` 함수의 반환값**

> 파이썬 2.7 버전까지 
> `a.keys() 함수`를 호출하면 리스트를 리턴한다. 
> (리스트를 리턴하기 위해서는 메모리 낭비가 발생)

> 파이썬 3.0 이후 버전 
> 메모리 낭비를 줄이기 위해 `dict_keys 객체`를 리턴하도록 변경
> 추가: `dict_values`, `dict_items`

<br>

**3) `dict_keys 객체` 사용하기**
* 리스트와 비슷하지만, `append()` `insert()` `pop()` `remove()` `sort()`함수는 사용할 수 없음
* `for문` 에서 사용하기

```python
for k in a.keys():
    print(k)

# result
# name
# phone
# birth
```

* `dict_keys 객체`를 `리스트`로 변환하기

```python
list(a.keys())	# ['name', 'phone', 'birth']
```

<br>
<br>

### **value 리스트를 만드는 `values()`**
 **1) `values()` 사용하기** 
 * `딕셔너리명.values()` : 해당 딕셔너리의 value 값만 모아  `dict_values 객체` 반환
 
```python
a.values()	# dict_values(['pey', '010-9999-1234', '1118'])
```


<br>
<br>


### **key, value 쌍을 반환하는 `items()`**
**1) `items()` 함수**
*  `key`와 `value`의 쌍을 튜플로 묶은 값을 `dict_items 객체`로 리턴
* `딕셔너리.items()`

```python
>>> a.items()
dict_items([('name', 'pey'), ('phone', '010-9999-1234'), ('birth', '1118')])
```

<br>
<br>

### **key: value 쌍을 모두 지우는 `clear()` 함수**
**1) `clear()` 함수**
* 딕셔너리 안의 모든 요소를 삭제
* `딕셔너리.clear()`

```python
a.clear()
print(a)	# {}
```

<br>
<br>


### **key를 사용해 value를 반환하는 `get()`함수**
**1) `get()`**
* `딕셔너리.get(key)` : key에 대응되는 value 리턴
* `dict.get('key')` ==  `dict['key']`
	*  딕셔너리에 존재하지 않는 키로 값을 가져오려고 할 경우,  `dick['key']`  방식은 오류를 발생
	* `dict.get('key')`  방식은 `None`을 리턴
* 딕셔너리 안에 찾으려는 key가 없을 경우, 미리 정해 둔 디폴트 값을 대신 가져오게 하고 싶을 때: ` dict.get(key, '디폴트 값')`

```python
a = {'name': 'pey', 'phone': '010-9999-1234', 'birth': '1118'}
print(a.get('name'))	# 'pey'
print(a.get('nokey'))	# None
print(a.get('nokey', 'foo'))	# 'foo'
```

<br>
<br>

### **해당 Key가 딕셔너리 안에 있는지 조사하는 `in()` 함수**
**1) `in()` 함수 사용하기**
* `key' in dict`
* 해당 key 가 딕셔너리 안에 있으면 True, 없으면 False 반환
```python
a = {'name':'pey', 'phone':'010-9999-1234', 'birth': '1118'}
print('name' in a)	# True
print('email' in a)	# False
```
