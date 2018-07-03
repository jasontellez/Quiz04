  # Quiz04


    def VecCheck(vector):
      """
      Takes a vector and checks whether each element is a number and prints its validity
      """
      validity = True
      for i in range(len(vector)):
        if ((type(vector[i]) != int) and (type(vector[i]) != float) and (type(vector[i]) != complex)):
        #condition for determining if vector contains the appropriate numbers
          Validity = False
          print("Invalid Input")
      return Validity
    def MatCheck(matrix):
      """
      Takes a matrix and calls VecCheck to check the matrix's validity through each row
      """
      Validity = True
      for j in range(len(matrix)):
        if VecCheck(matrix[j]) != True:
          Validity = False
          return Validity
      print("Validity")

    def dot(vector01,vector02):
      """
      Inputs 2 vectors as arguments and returns the dot product of those vectors. This is done by first checking for the condition of the vectors being of equal dimensions. If the condition is met, the vectors are iterated through a for-loop so that each element in the list is multiplied by its respectively positioned element in the opposite vector. If the conditio is not met, the string 'invalid input' is returned.
      """
      dotPro = 0 #empty value for storing data
      if VecCheck(vector01) == True and VecCheck(vector02) == True and range(len(vector01)) == range(len(vector02)):  #condition that requires vectors to have same dimensions
        for i in range(len(vector01)):  #iterates through rows of vector01
          dotPro += vector01[i]*vector02[i] #multiplies elements of each vector and adds products
        return dotPro
      else: #condition for when dimensions are unequal
        print("Invalid Input")

    def vecSubtract(vector01,vector02):
      """
      A function that perfroms vector subtraction by iterating through the elements within the vectors and iteratively subtracts the elements from one vector to the other. Finally, the resulting vector is stored in an empty list and printed.
      """
      element = 0 #empty value for storing values of elements
      sub = []  #empty list for storing resulting vector
      if VecCheck(vector01) == True and VecCheck(vector02) == True and len(vector01) == len(vector02):  #condition that requires vectors to have same dimensions
        for i in range(len(vector01)):  ##iterates through rows of vector01
          element = vector01[i]-vector02[i] #stores values of individual elements
          sub.append(element) #creates new list from empty list
        return sub
      else:
        print("Invalid Input")

    def ScalarVecMulti(scalar,vector):
      """
      Function that inputs a vector aqnd a scalar and multiplies the values to return a new vector.
      This is done via a for-loop by stroing the new values inside premade empty values
      """
      element = 0 #empty value for storing elements of new vector
      product = []  #empty list for stoing new vector
      if VecCheck(vector01) == True:
        for i in range(len(vector)):  #iterates through rows of vector
          element = scalar*vector[i]  #stores new values from the proudct of the scalar and each element of the vector
          product.append(element) #adds values of vector to empty list
        return product

    def twoNorm(vector):
      """
      twoNorm takes a vector as it's argument. It then computes the sum of  the squares of each element of the vector. It then returns the square root of this sum.
      """
      # This variable will keep track of the validity of our input.
      inputStatus = True  
      # This for loop will check each element of the vector to see if it's a number. 
      for i in range(len(vector)):  
        if ((type(vector[i]) != int) and (type(vector[i]) != float) and (type(vector[i]) != complex)):
          inputStatus = False
          print("Invalid Input")
      # If the input is valid the function continues to compute the 2-norm
      if inputStatus == True:
        result = 0
        # This for loop will compute the sum of the squares of the elements of the vector. 
        for i in range(len(vector)):
          result = result + (vector[i]**2)
        result = result**(1/2)
        return result

    def matVec(matrix,vector):
      """
      This function takes matrix and a vector, multiplies htme together, and then returns the matrix-vector product. 
      """
      if MatCheck(matrix) == True and VecCheck(vector) == True and len(matrix) == len(vector):
      # Ensures that the matrix and vector are dimensionally compatible.
        for i in range(len(matrix)):
          product = []
          # an empty list for the result (i.e. the result/product/b)
          row_var = 0
          # a value that will be used for the variables for the resulting matrix
          for j in range(len(vector)):
            row_var += matrix[i][j] * vector[j]
            product.append(row_var)
          return product
      else:
        print("Incompatible dimensions")

    def normalize(vector):
      """
      A function that utilizes the previously defined infNorm function that iterates through the elements of a vector and using aritmetic with a scalar to form a normalized vector with respect to the norm. Once the values are created, the new elements are stored in an empty list using the .append function and finally the result is printed.
      """
      norm = twoNorm(vector)  #calls value from previous function
      normed = [] #empty list for storing normalized vector
      for i in vector:  #iterates through the elements of the vector
        normed.append((1/norm)*i) #adds values of the vector to the empty list
      return normed

    def ModGS(matrix):	
      """
      Inputs a matrix, checks the validity of its elements, and finds the Modified Gram-Schmidt QR-factorization of a matrix and returns theQ and R matrices. This is performed by creating empty matrices and iterating through the colmuns of a matrix, intializing various operations, and filling the empty lists with the respective elements.
      """
      if MatCheck(matrix) == True:
        m = len(matrix[0])	#creates value for number of rows in matrix
        n = len(matrix)	#value of columns in matrix
        V = matrix
        R = [[0] * n for i in range(n)]	#creates an empty nxn matrix
        Q = [[0] * m for i in range(n)]	#creates empty mxn matrix
        for i in range(n):
          R[i][i] = twoNorm(V[i])	#finds the 2-norm of V
          Q[i] = normalize(V[i])	#finds the normalized value of the clomuns of V
          for j in range(i + 1, n):
            R[j][i] = dot(Q[i],V[j])	#finds the dot-product of the columns of Q and V
            temp = ScalarVecMulti(R[j][i],Q[i])	#finds the scalar-vector mulitplication of the R and Q
            V[j] = vecSubtract(V[j], temp)
        return[Q,R]
      else:
        print("Invalid Input")
