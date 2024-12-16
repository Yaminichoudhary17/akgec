Solution1:

/******************************************************************************

                            Online Java Compiler.
                Code, Compile, Run and Debug java program online.
Write your code in this editor and press "Run" button to execute it.

*******************************************************************************/

public class Main
{
	public static void main(String[] args) {
		System.out.println("Hello World");
		 int n = 7;

    for (int i = 0; i < 2 * n - 1; i++) {

        
        int c;
        if (i < n) {
            c = 2 * (n - i) - 1;
        }
        else {
            c = 2 * (i - n + 1) + 1;
        }

        for (int j = 0; j < c; j++) {
            System.out.print(" ");
        }

        for (int k = 0; k < 2 * n - c; k++) {
           System.out.print("* ");
        }
        System.out.print("\n");
    }
	}
}



solution2
/******************************************************************************

                            Online Java Compiler.
                Code, Compile, Run and Debug java program online.
Write your code in this editor and press "Run" button to execute it.

*******************************************************************************/
import java.util.*;
public class Main
{

    public static void main(String[] args) {
       
        int[] arr1 = {5, 1, 8, 11, 2};
        

      
        System.out.println(Arrays.toString(sortArray(arr1)));
    }

    
    public static boolean isPrime(int num) {
        if (num <= 1) return false; 
        for (int i = 2; i <= Math.sqrt(num); i++) {
            if (num % i == 0) return false; 
        }
        return true;
    }

    
    public static int[] sortArray(int[] arr) {
        List<Integer> primes = new ArrayList<>();
        List<Integer> nonPrimes = new ArrayList<>();
        
        
        for (int num : arr) {
            if (isPrime(num)) {
                primes.add(num);
            } else {
                nonPrimes.add(num);
            }
        }
        
        
        Collections.sort(primes, Collections.reverseOrder());
        
        Collections.sort(nonPrimes, Collections.reverseOrder());
        
        int[] result = new int[arr.length];
        
        
        result[0] = primes.get(0);  
        result[arr.length - 1] = primes.get(primes.size() - 1);
        
        
        int index = 1;
        for (int i = 1; i < primes.size() - 1; i++) {
            result[index++] = primes.get(i);
        }
        
        
        for (int num : nonPrimes) {
            result[index++] = num;
        }

        return result;
    }
}



Solution3
import React, { useState, useEffect } from "react";


const EmployeeList = ({ employees }) => {
  return (
    <div>
      <h2>Employee List</h2>
      <ul>
        {employees.map((employee) => (
          <li key={employee.id}>
            {employee.name} ({employee.email})
          </li>
        ))}
      </ul>
    </div>
  );
};


const RegisterForm = ({ onSubmit }) => {
  const [formData, setFormData] = useState({
    name: "",
    email: "",
  });

  const handleChange = (e) => {
    const { name, value } = e.target;
    setFormData({
      ...formData,
      [name]: value,
    });
  };

  const handleSubmit = async (e) => {
    e.preventDefault();
    await onSubmit(formData);
    setFormData({ name: "", email: "" });
  };

  return (
    <form onSubmit={handleSubmit} className="form">
      <div className="form-group">
        <label htmlFor="name">Name</label>
        <input
          type="text"
          id="name"
          name="name"
          value={formData.name}
          onChange={handleChange}
          required
        />
      </div>
      <div className="form-group">
        <label htmlFor="email">Email</label>
        <input
          type="email"
          id="email"
          name="email"
          value={formData.email}
          onChange={handleChange}
          required
        />
      </div>
      <button type="submit">Submit</button>
    </form>
  );
};

function App() {
  const [employees, setEmployees] = useState([]);
  const [isLoading, setIsLoading] = useState(true);

  useEffect(() => {
    const fetchEmployees = async () => {
      try {
        const response = await axios.get(
          "https://jsonplaceholder.typicode.com/users"
        );
        setEmployees(response.data);
      } catch (error) {
        console.error("Error fetching employees:", error);
      } finally {
        setIsLoading(false);
      }
    };

    fetchEmployees();
  }, []);

  const handleRegisterSubmit = async (formData) => {
    try {
      const response = await axios.post(
        "https://jsonplaceholder.typicode.com/users",
        formData
      );
      console.log("User registered:", response.data);
      alert("Registration successful!");
    } catch (error) {
      console.error("Error registering user:", error);
    }
  };

  return (
    <div className="App">
      <h1>Registration Form</h1>
      <RegisterForm onSubmit={handleRegisterSubmit} />
      {isLoading ? (
        <p>Loading employees...</p>
      ) : (
        <EmployeeList employees={employees} />
      )}
    </div>
  );
}

export default App;

