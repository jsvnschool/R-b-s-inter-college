import sqlite3

# --- DATABASE SETUP ---
conn = sqlite3.connect("js_vidya_niketan.db")
cursor = conn.cursor()

# Database Table Setup
cursor.execute("""
CREATE TABLE IF NOT EXISTS students (
    roll_no TEXT PRIMARY KEY,
    name TEXT NOT NULL,
    class_name TEXT NOT NULL,
    maths_fa1 REAL DEFAULT 0, maths_fa2 REAL DEFAULT 0, maths_sa1 REAL DEFAULT 0,
    maths_fa3 REAL DEFAULT 0, maths_fa4 REAL DEFAULT 0, maths_sa2 REAL DEFAULT 0,
    sci_fa1 REAL DEFAULT 0, sci_fa2 REAL DEFAULT 0, sci_sa1 REAL DEFAULT 0,
    sci_fa3 REAL DEFAULT 0, sci_fa4 REAL DEFAULT 0, sci_sa2 REAL DEFAULT 0,
    eng_fa1 REAL DEFAULT 0, eng_fa2 REAL DEFAULT 0, eng_sa1 REAL DEFAULT 0,
    eng_fa3 REAL DEFAULT 0, eng_fa4 REAL DEFAULT 0, eng_sa2 REAL DEFAULT 0,
    hin_fa1 REAL DEFAULT 0, hin_fa2 REAL DEFAULT 0, hin_sa1 REAL DEFAULT 0,
    hin_fa3 REAL DEFAULT 0, hin_fa4 REAL DEFAULT 0, hin_sa2 REAL DEFAULT 0
)
""")
conn.commit()


# --- FUNCTIONS ---


def add_student():
    print("\n--- NEW STUDENT REGISTRATION ---")
    roll = input("Roll Number dalo: ")
    name = input("Student Name dalo: ")
    cls = input("Class dalo: ")

    try:
        cursor.execute(
            "INSERT INTO students (roll_no, name, class_name) VALUES (?, ?, ?)",
            (roll, name, cls),
        )
        conn.commit()
        print(
            f"✅ Student {name} (Roll No: {roll}) System me Add Ho Gaya Hai!"
        )
    except sqlite3.IntegrityError:
        print("❌ Is Roll Number ka student pehle se majood hai!")


def enter_marks():
    print("\n--- MARKS ENTRY SYSTEM (FA1, FA2, SA1, FA3, FA4, SA2) ---")
    roll = input("Marks enter karne ke liye Roll Number dalo: ")

    cursor.execute("SELECT name, class_name FROM students WHERE roll_no = ?", (roll,))
    student = cursor.fetchone()

    if not student:
        print("❌ Student Nahi Mila! Pehle Roll Number Add Karein.")
        return

    print(f"\nStudent Found: {student[0]} | Class: {student[1]}")
    print("\nExam Type Chuno:")
    print("1. FA1 (10 Marks Max)")
    print("2. FA2 (10 Marks Max)")
    print("3. SA1 (30 Marks Max)")
    print("4. FA3 (10 Marks Max)")
    print("5. FA4 (10 Marks Max)")
    print("6. SA2 (30 Marks Max)")

    exam_opt = input("Option No. Dalo (1-6): ")
    exam_map = {
        "1": "fa1",
        "2": "fa2",
        "3": "sa1",
        "4": "fa3",
        "5": "fa4",
        "6": "sa2",
    }

    if exam_opt not in exam_map:
        print("❌ Galat option!")
        return

    exam_type = exam_map[exam_opt]

    print(f"\n--- Entering Marks for Exam: {exam_type.upper()} ---")
    m_math = float(input("Mathematics Marks: "))
    m_sci = float(input("Science Marks: "))
    m_eng = float(input("English Marks: "))
    m_hin = float(input("Hindi Marks: "))

    query = f"""
        UPDATE students 
        SET maths_{exam_type} = ?, sci_{exam_type} = ?, eng_{exam_type} = ?, hin_{exam_type} = ?
        WHERE roll_no = ?
    """
    cursor.execute(query, (m_math, m_sci, m_eng, m_hin, roll))
    conn.commit()
    print(f"✅ {exam_type.upper()} ke Marks Safaltapoorvak Save Ho Gaye!")


def generate_marksheet():
    print("\n--- GENERATE PROFESSIONAL MARKSHEET ---")
    roll = input("Marksheet ke liye Roll Number Dalo: ")

    cursor.execute("SELECT * FROM students WHERE roll_no = ?", (roll,))
    row = cursor.fetchone()

    if not row:
        print("❌ Is Roll Number ka student nahi mila!")
        return

    # Data Extracting
    roll_no, name, class_name = row[0], row[1], row[2]
    m_m = row[3:9]  # Maths: FA1, FA2, SA1, FA3, FA4, SA2
    m_s = row[9:15]  # Science
    m_e = row[15:21]  # English
    m_h = row[21:27]  # Hindi

    # Totals Calculation
    math_tot = sum(m_m)
    sci_tot = sum(m_s)
    eng_tot = sum(m_e)
    hin_tot = sum(m_h)

    grand_total = math_tot + sci_tot + eng_tot + hin_tot
    percentage = (grand_total / 400) * 100

    if percentage >= 75:
        grade = "A+ (Distinction)"
    elif percentage >= 60:
        grade = "A (First Division)"
    elif percentage >= 50:
        grade = "B (Second Division)"
    elif percentage >= 33:
        grade = "C (Third Division)"
    else:
        grade = "F (Needs Improvement)"

    # PRINT MARKSHEET FORMAT
    print("\n" + "=" * 78)
    print("                    J.S. VIDYA NIKETAN                    ".center(78))
    print(
        "    Radha Krishna Maholla, Aliganj, Etah (U.P.) - 207247    ".center(
            78
        )
    )
    print("                   ANNUAL PERFORMANCE REPORT CARD                 ")
    print("=" * 78)
    print(f" Student Name : {name:<30} Roll No. : {roll_no}")
    print(f" Class        : {class_name:<30} Session  : 2025-2026")
    print("-" * 78)
    print(
        f"{'SUBJECT':<15} | {'FA1':<4} | {'FA2':<4} | {'SA1':<4} | {'FA3':<4} | {'FA4':<4} | {'SA2':<4} | {'TOTAL (100)':<11}"
    )
    print("-" * 78)

    print(
        f"{'Mathematics':<15} | {m_m[0]:<4} | {m_m[1]:<4} | {m_m[2]:<4} | {m_m[3]:<4} | {m_m[4]:<4} | {m_m[5]:<4} | {math_tot:<11.1f}"
    )
    print(
        f"{'Science':<15} | {m_s[0]:<4} | {m_s[1]:<4} | {m_s[2]:<4} | {m_s[3]:<4} | {m_s[4]:<4} | {m_s[5]:<4} | {sci_tot:<11.1f}"
    )
    print(
        f"{'English':<15} | {m_e[0]:<4} | {m_e[1]:<4} | {m_e[2]:<4} | {m_e[3]:<4} | {m_e[4]:<4} | {m_e[5]:<4} | {eng_tot:<11.1f}"
    )
    print(
        f"{'Hindi':<15} | {m_h[0]:<4} | {m_h[1]:<4} | {m_h[2]:<4} | {m_h[3]:<4} | {m_h[4]:<4} | {m_h[5]:<4} | {hin_tot:<11.1f}"
    )

    print("-" * 78)
    print(
        f" GRAND TOTAL : {grand_total:.1f} / 400 | PERCENTAGE : {percentage:.2f}% | GRADE : {grade}"
    )
    print("=" * 78)
    print(" Result Status : PASSED" if percentage >= 33 else " Result Status : FAILED")
    print("\n Sign (Class Teacher)                         Sign (Principal)")
    print("=" * 78 + "\n")


# --- MAIN MENU LOOP ---
def main():
    while True:
        print("\n========================================================")
        print("    J.S. VIDYA NIKETAN - SCHOOL MANAGEMENT SYSTEM       ")
        print("========================================================")
        print("1. Add New Student")
        print("2. Enter Subject Marks (FA1, FA2, SA1, FA3, FA4, SA2)")
        print("3. Search & Generate Marksheet")
        print("4. Exit Program")

        choice = input("\nSelect Option (1-4): ")

        if choice == "1":
            add_student()
        elif choice == "2":
            enter_marks()
        elif choice == "3":
            generate_marksheet()
        elif choice == "4":
            print(
                "\nSystem successfully closed. Data has been safely stored in Database!"
            )
            conn.close()
            break
        else:
            print("❌ Invalid Option! Sahi option chunein.")


if __name__ == "__main__":
    main()
