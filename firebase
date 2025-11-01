import { useEffect, useState } from "react";
import {getDatabase, ref, push, onValue} from 'firebase/database';
import { initializeApp } from "firebase/app";

const firebaseConfig = {
  apiKey: "AIzaSyDYznb0MpjNYpZH4mF1rwKERZk8aYRR3Vk",
  authDomain: "student-management-fd5ef.firebaseapp.com",
  databaseURL: "https://student-management-fd5ef-default-rtdb.firebaseio.com",
  projectId: "student-management-fd5ef",
  storageBucket: "student-management-fd5ef.firebasestorage.app",
  messagingSenderId: "447868692051",
  appId: "1:447868692051:web:ad19137c8a8f18852ec8a6",
  measurementId: "G-TPK7TVEC64"
};

const app = initializeApp(firebaseConfig);
const db = getDatabase(app, "https://student-management-fd5ef-default-rtdb.firebaseio.com/");
const studentRef = ref(db, 'students');

export default function App(){
    const [students, setStudents] = useState([]);
    const [name, setName] = useState('');
    const [course, setCourse] = useState('');
    const [loading, setLoading] = useState(true);

    useEffect(()=>{
        const unsubscribe = onValue(studentRef, (snapshot)=>{
            const data = snapshot.val();
            const studentList = [];
            if(data){
                for(const key in data)
                    studentList.push({ id: key, ...data[key] });
            }
            setStudents(studentList);
            setLoading(false);
        });

        return () => unsubscribe();
    }, []);

    const handleSubmit = (e) => {
        e.preventDefault();
        if(name && course){
            push(studentRef, {name, course});
            setName('');
            setCourse('');
        }
    };

    return(
        <div>
            <form onSubmit={handleSubmit}>
                <input type="text" value={name} onChange={(e) => setName(e.target.value)} placeholder="name"/>
                <input type="text" value={course} onChange={(e) => setCourse(e.target.value)} placeholder="course"/>
                <button type="submit">Submit</button>
            </form>
            <div>
                <h3>Student List</h3>
                {loading && <p>Loading...</p>}
                <ul>
                    {students.map(student => (
                        <li key={student.id}>
                            {student.name} - {student.course}
                        </li>
                    ))}
                </ul>
            </div>
        </div>
    );
}