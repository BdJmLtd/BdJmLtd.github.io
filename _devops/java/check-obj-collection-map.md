---
title: "检查 Object、Collection、Map是否为空"
sequence: 101
---

## Object

### 检查对象是否为空

第一种方式，使用 JDK 内置的 `java.util.Objects` 类：

```java
public final class Objects {
    public static boolean isNull(Object obj) {
        return obj == null;
    }

    public static boolean nonNull(Object obj) {
        return obj != null;
    }
}
```

第二种方式，使用 `commons-lang3-3.x.x.jar` 的 `org.apache.commons.lang3.ObjectUtils` 类：

```java
public class ObjectUtils {
    public static boolean isEmpty(final Object object) {
        if (object == null) {
            return true;
        }
        if (object instanceof CharSequence) {
            return ((CharSequence) object).length() == 0;
        }
        if (object.getClass().isArray()) {
            return Array.getLength(object) == 0;
        }
        if (object instanceof Collection<?>) {
            return ((Collection<?>) object).isEmpty();
        }
        if (object instanceof Map<?, ?>) {
            return ((Map<?, ?>) object).isEmpty();
        }
        return false;
    }

    public static boolean isNotEmpty(final Object object) {
        return !isEmpty(object);
    }
}
```

## Collection

### 检查集合是否为空

使用 `commons-collections4-4.x.jar` 的 `org.apache.commons.collections4.CollectionUtils` 类：

```java
public class CollectionUtils {
    public static boolean isEmpty(final Collection<?> coll) {
        return coll == null || coll.isEmpty();
    }

    public static boolean isNotEmpty(final Collection<?> coll) {
        return !isEmpty(coll);
    }
}
```

### 返回空的集合

使用 JDK 内置的 `java.util.Collections` 类：

```java
public class Collections {
    public static final List EMPTY_LIST = new EmptyList<>();
    
    public static final <T> List<T> emptyList() {
        return (List<T>) EMPTY_LIST;
    }

    public static final <T> Set<T> emptySet() {
        return (Set<T>) EMPTY_SET;
    }
}
```

## Map

### 检查 Map 是否为空

使用 `commons-collections4-4.x.jar` 的 `org.apache.commons.collections4.MapUtils` 类：

```java
public class MapUtils {
    public static boolean isEmpty(final Map<?,?> map) {
        return map == null || map.isEmpty();
    }

    public static boolean isNotEmpty(final Map<?,?> map) {
        return !MapUtils.isEmpty(map);
    }
}
```

### 返回空的Map

使用 JDK 内置的 `java.util.Collections` 类：

```java
public class Collections {
    public static final Map EMPTY_MAP = new EmptyMap<>();

    public static final <K,V> Map<K,V> emptyMap() {
        return (Map<K,V>) EMPTY_MAP;
    }
}
```
