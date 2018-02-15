# Leetcode: Flatten 2D Vector     :BLOG:Medium:


---

Flatten 2D Vector  

---

Similar Problems:  

-   [Design Compressed String Iterator](https://brain.dennyzhang.com/design-compressed-string-iterator)
-   [Flatten Nested List Iterator](https://brain.dennyzhang.com/flatten-nested-list-iterator)
-   Tag: [#designquestion](https://brain.dennyzhang.com/tag/designquestion)

---

Implement an iterator to flatten a 2d vector.  

For example,  

    Given 2d vector =
    
    [
      [1,2],
      [3],
      [4,5,6]
    ]

By calling next repeatedly until hasNext returns false, the order of elements returned by next should be: [1,2,3,4,5,6].  

Follow up:  
As an added challenge, try to code it using only iterators in C++ or iterators in Java.  

Github: [challenges-leetcode-interesting](https://github.com/DennyZhang/challenges-leetcode-interesting/tree/master/flatten-2d-vector)  

Credits To: [leetcode.com](https://leetcode.com/problems/flatten-2d-vector/description/)  

Leave me comments, if you have better ways to solve.  

    ## Blog link: https://brain.dennyzhang.com/flatten-2d-vector
    ## Basic Ideas: Caching current element
    ##
    ##   Sample Data: some elements may look like [[1], , [2, 3]]
    ##   Assumption: return None, if unexpected input/call
    ##
    ## Complexity:
    class Vector2D(object):
    
        def __init__(self, vec2d):
            """
            Initialize your data structure here.
            :type vec2d: List[List[int]]
            """
            self.vec2d = vec2d
            self.row, self.col = 0, 0
    
        def next(self):
            """
            :rtype: int
            """
            if self.hasNext() is False: return None
            self.col += 1
            return self.vec2d[self.row][self.col-1]
    
        def hasNext(self):
            """
            :rtype: bool
            """
            while self.row < len(self.vec2d) and self.col == len(self.vec2d[self.row]):
                self.col, self.row = 0, self.row + 1
    
            return self.row != len(self.vec2d)
    # Your Vector2D object will be instantiated and called as such:
    # i, v = Vector2D(vec2d), 
    # while i.hasNext(): v.append(i.next())