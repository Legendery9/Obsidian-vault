```java
private boolean containsId(int id) {
    return students.stream()
        .anyMatch(student -> student.getId() == id);
}
```