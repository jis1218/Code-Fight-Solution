For the upcoming academic year the Coolcoders University should decide which students will get the scholarships. Scholarships are considered to be correctly distributed if all best students have it, but not all students in the university do. Obviously, only university students should be able to get a scholarship, i.e. there should be no outsiders in the list of the students that will get a scholarships.
You are given lists of unique student ids bestStudents, scholarships and allStudents, representing ids of the best students, students that will get a scholarship and all the students in the university, respectively. Return true if the scholarships are correctly distributed and false otherwise.
Example
For bestStudents = [3, 5], scholarships = [3, 5, 7] and
allStudents = [1, 2, 3, 4, 5, 6, 7], the output should be
correctScholarships(bestStudents, scholarships, allStudents) = true;
For bestStudents = [3, 5], scholarships = [3, 5] and
allStudents = [3, 5], the output should be
correctScholarships(bestStudents, scholarships, allStudents) = false.
All students get a scholarship, which is not correct.
For bestStudents = [3], scholarships = [1, 3, 5] and
allStudents = [1, 2, 3], the output should be
correctScholarships(bestStudents, scholarships, allStudents) = false.
There's no student with id 5, yet somehow he managed to get a scholarship.

##### 나의 풀이 - set을 사용하여 풀었다. 좀 복잡하게 푼 감이 있다.
```python
def correctScholarships(bestStudents, scholarships, allStudents):
    return sorted(list(set(bestStudents).intersection(set(scholarships)))) == sorted(bestStudents) and \
(sorted(list(set(scholarships).union(set(allStudents)))) == sorted(allStudents) and (sorted(list(set(scholarships).intersection(set(allStudents)))) != sorted(allStudents)))
```

##### 나와 비슷하게 접근한 풀이
```python
def correctScholarships(bestStudents, scholarships, allStudents):
    return set(bestStudents).issubset(set(scholarships))and set(scholarships)!=set(allStudents) and set(scholarships).issubset(set(allStudents))
```

##### 최고의 풀이
```python
def correctScholarships(bestStudents, scholarships, allStudents):
    return set(bestStudents) <= set(scholarships) < set(allStudents)
```