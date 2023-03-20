### Introduction

Write the following functions:

1.  `makeCacheMatrix`: This function creates a special "matrix" object
    that can cache its inverse.
2.  `cacheSolve`: This function computes the inverse of the special
    "matrix" returned by `makeCacheMatrix` above. If the inverse has
    already been calculated (and the matrix has not changed), then
    `cacheSolve` should retrieve the inverse from the cache.

### 1: Caching the Mean of a Matrix

The first function, `makeMatrix` creates a special "Matrix", which is
really a list containing a function to

1.  set the value of the matrix
2.  get the value of the matrix
3.  set the inverse of the matrix
4.  get the inverse of the matrix

<!-- -->

    makeCacheMatrix <- function(x = matrix()) {
      m <- NULL
      set <- function(y) {
        x <<- y
        m <<- NULL
      }
      get <- function() x
      setInverse <- function(inverse) m <<- inverse
      getInverse <- function() m
      list(set = set, get = get,
           setInverse = setInverse,
           getInverse = getInverse)
    }

The following function computes the inverse of the special "Matrix"
created with the above function. However, it first checks to see if the
mean has already been calculated. If so, it `get`s the inverse from the
cache and skips the computation. Otherwise, it calculates the inverse of
the matrix and sets the value of the inverse in the cache via the `setinverse`
function.

    cacheSolve <- function(x, ...) {
      m <- x$getInverse()
      if(!is.null(m)) {
        message("getting cached data")
        return(m)
      }
      data <- x$get()
      m <- solve(data, ...)
      x$setInverse(m)
      m
    }

### Assignment: Caching the Inverse of a Matrix

### Test the code:
### my_matrix <- makeCacheMatrix(matrix(1:4,nrow =2,ncol = 2))
### my_matrix$get()
### my_matrix$getInverse()
### cacheSolve(my_matrix)



