### `getOrDefault`
찾는 키가 존재하면 값을 반환하고 없으면 기본 값을 반환

```
default V getOrDefault(Object key, V defaultValue)
```

### `entrySet`과 `keySet`
https://stackoverflow.com/questions/3870064/performance-considerations-for-keyset-and-entryset-of-map

- if you're concerned about performance when iterating through your hash map, I suggest you have a look at `LinkedHashMap`.

```java
for (Object key : map.keySet()) {
    Object value = map.get(key);
}
```
이렇게 쓰는 것보다

```java
for (Map.Entry entry : map.entrySet()) {
    Object key = entry.getKey();
    Object value = entry.getValue();
}
```

이렇게 사용하는 것이 더 효율적이라고 함

> Because in the second case, for every key in the keySet the map.get() method is called, which - in the case of a HashMap - requires that the hashCode() and equals() methods of the key object be evaluated in order to find the associated value*. In the first case that extra work is eliminated.
