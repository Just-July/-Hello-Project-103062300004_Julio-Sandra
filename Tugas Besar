package main

import (
	"bufio"
	"encoding/json"
	"fmt"
	"os"
)

type Nilai struct {
	Uts   float64
	Uas   float64
	Quiz  float64
	Total float64
	Grade string
}

type Matakuliah struct {
	Subject string
	Grades  Nilai
}

type Mahasiswa struct {
	Nama       string
	Nim        string
	Sks        int
	Nilai      float64
	Matakuliah []Matakuliah
}

func telkomAsciiArt() {
	asciiArt := `
  _____ _____ _     _  _____  __  __           _   _ _   _ _____     _______ ____  ____ ___ _______   __
 |_   _| ____| |   | |/ / _ \|  \/  |         | | | | \ | |_ _\ \   / / ____|  _ \/ ___|_ _|_   _\ \ / /
   | | |  _| | |   | ' / | | | |\/| |  _____  | | | |  \| || | \ \ / /|  _| | |_) \___ \| |  | |  \ V / 
   | | | |___| |___| . \ |_| | |  | | |_____| | |_| | |\  || |  \ V / | |___|  _ < ___) | |  | |   | |  
   |_| |_____|_____|_|\_\___/|_|  |_|          \___/|_| \_|___|  \_/  |_____|_| \_\____/___| |_|   |_|                                                                         
	`
	fmt.Println(asciiArt)
}

func rocketAsciiArt() {
	fmt.Println("                                                   *     .--.")
	fmt.Println("                                                        / /  `")
	fmt.Println("                                       +               | |")
	fmt.Println("                                              '         \\ \\__,")
	fmt.Println("                                          *          +   '--'  *")
	fmt.Println("                                              +   /\\")
	fmt.Println("                                 +              .'  '.   *")
	fmt.Println("                                        *      /======\\      +")
	fmt.Println("                                              ;:.  _   ;")
	fmt.Println("                                              |:. (_)  |")
	fmt.Println("                                              |:.  _   |")
	fmt.Println("                                    +         |:. (_)  |          *")
	fmt.Println("                                              ;:.      ;")
	fmt.Println("                                            .' \\:.    / `.")
	fmt.Println("                                           / .-''':._.'`-. \\")
	fmt.Println("                                           |/    /||\\    \\|")
	fmt.Println("                                        _..--\"\"\"````\"\"\"--.._")
	fmt.Println("                                   _.-'``                    ``'-._")
	fmt.Println("                                 -'                                '-")
}

func kelompokAsciiArt() {
	ascii := `  ___         _  __    _                     _     _ _  
 | _ )_  _   | |/ /___| |___ _ __  _ __  ___| |__ | | | 
 | _ \ || |  | ' </ -_) / _ \ '  \| '_ \/ _ \ / / |_  _|
 |___/\_, |  |_|\_\___|_\___/_|_|_| .__/\___/_\_\   |_| 
      |__/                        |_|                   `
	fmt.Println(ascii)
}

func waitForKeypress() {
	fmt.Println("Press Enter to continue...")
	bufio.NewReader(os.Stdin).ReadBytes('\n')
}

func menu() {
	fmt.Println("--------------------------------------------------")
	fmt.Println("| 1. Data Seluruh Mahasiswa                      |")
	fmt.Println("| 2. Input Data Mahasiswa Baru                   |")
	fmt.Println("| 3. Edit Data Mahasiswa                         |")
	fmt.Println("| 4. Add Matakuliah Mahasiswa                    |")
	fmt.Println("| 5. Delete Matakuliah Mahasiswa                 |")
	fmt.Println("| 6. Display Transkrip Mahasiswa                 |")
	fmt.Println("| 7. Tampilkan Mahasiswa Berdasarkan Mata Kuliah |")
	fmt.Println("| 8. Tampilkan Mata Kuliah Berdasarkan Mahasiswa |")
	fmt.Println("| 9. Tampilkan Mahasiswa Secara Terurut          |")
	fmt.Println("| 0. Exit program                                |")
	fmt.Println("--------------------------------------------------")
	fmt.Printf("Enter Your Choice: ")
}

func main() {
	students := loadFromFile("students.json")
	running := true
	telkomAsciiArt()
	rocketAsciiArt()
	kelompokAsciiArt()
	fmt.Printf("\n")
	for running {
		var op int
		menu()
		fmt.Scan(&op)
		bufio.NewScanner(os.Stdin).Scan()
		switch op {
		case 1:
			displayAll(students)
		case 2:
			inputData(&students)
		case 3:
			editData(students)
		case 4:
			addSubject(&students)
		case 5:
			deleteSubject(&students)
		case 6:
			displayTranscript(students)
		case 7:
			displayStudentsBySubject(students)
		case 8:
			displaySubjectsByStudent(students)
		case 9:
			if len(students) == 0 {
				fmt.Printf("Data Kosong!\n")
			} else {
				rocket_sort(students)
			}
			waitForKeypress()
		case 0:
			var save string
			fmt.Printf("Do you want to save this file? (y/n): ")
			fmt.Scan(&save)
			if save == "y" || save == "Y" {
				saveToFile(students, "students.json")
				fmt.Printf("File was successfully saved. Exiting program...\n")
			}
			running = false
		default:
			fmt.Println("INVALID INPUT!")
		}
	}
}

func loadFromFile(filename string) []Mahasiswa {
	file, err := os.Open(filename)
	if err != nil {
		fmt.Println("No existing data found, starting fresh.")
		return []Mahasiswa{}
	}
	defer file.Close()

	var students []Mahasiswa
	decoder := json.NewDecoder(file)
	err = decoder.Decode(&students)
	if err != nil {
		fmt.Println("Error decoding data, starting fresh.")
		return []Mahasiswa{}
	}
	return students
}

func saveToFile(students []Mahasiswa, filename string) {
	file, err := os.Create(filename)
	if err != nil {
		fmt.Println("Error creating file:", err)
		return
	}
	defer file.Close()

	encoder := json.NewEncoder(file)
	err = encoder.Encode(students)
	if err != nil {
		fmt.Println("Error encoding data:", err)
	}
}

func rocket_sort(arr []Mahasiswa) {
	students := make([]Mahasiswa, len(arr))
	copy(students, arr)
	n := len(students)
	for i := 0; i < n-1; i++ {
		for j := 0; j < n-i-1; j++ {
			if students[j].Sks < students[j+1].Sks {
				students[j], students[j+1] = students[j+1], students[j]
			} else if students[j].Sks == students[j+1].Sks {
				if students[j].Nilai < students[j+1].Nilai {
					students[j], students[j+1] = students[j+1], students[j]
				}
			}
		}
	}
	i := 1
	fmt.Println("-------------------------------------------------")
	for _, student := range students {
		fmt.Printf("%d. Nama: %s, NIM: %s, SKS: %d, Nilai: %.2f\n", i, student.Nama, student.Nim, student.Sks, student.Nilai)
		i++
	}
	fmt.Println("-------------------------------------------------")
}

func displayTranscript(students []Mahasiswa) {
	var NIM string
	fmt.Printf("Masukkan NIM mahasiswa: ")
	fmt.Scan(&NIM)

	for _, student := range students {
		if student.Nim == NIM {
			fmt.Printf("-------------------------------------------------\n")
			fmt.Printf("Transkrip Nilai untuk %s (NIM: %s):\n", student.Nama, student.Nim)
			fmt.Printf("Total SKS: %d\n", student.Sks)
			for _, matkul := range student.Matakuliah {
				fmt.Printf("Mata Kuliah: %s\n", matkul.Subject)
				fmt.Printf("Nilai UTS: %.2f\n", matkul.Grades.Uts)
				fmt.Printf("Nilai UAS: %.2f\n", matkul.Grades.Uas)
				fmt.Printf("Nilai Quiz: %.2f\n", matkul.Grades.Quiz)
				fmt.Printf("Total nilai: %.2f\n", matkul.Grades.Total)
				fmt.Printf("Grade: %s\n", matkul.Grades.Grade)
				fmt.Println("-------------------------------------------------")
			}
			waitForKeypress()
			return
		}
	}
	fmt.Println("Mahasiswa dengan NIM tersebut tidak ditemukan!")
	waitForKeypress()
}

func addSubject(students *[]Mahasiswa) {
	var NIM string
	scanner := bufio.NewScanner(os.Stdin)
	fmt.Printf("Masukkan NIM mahasiswa yang ingin ditambahkan mata kuliah: ")
	fmt.Scan(&NIM)
	bufio.NewScanner(os.Stdin).Scan()

	for i := range *students {
		if (*students)[i].Nim == NIM {
			var matkul Matakuliah
			fmt.Printf("Input nama mata kuliah: ")
			scanner.Scan()
			matkul.Subject = scanner.Text()
			fmt.Printf("Input nilai UTS untuk %s: ", matkul.Subject)
			fmt.Scan(&matkul.Grades.Uts)
			fmt.Printf("Input nilai UAS untuk %s: ", matkul.Subject)
			fmt.Scan(&matkul.Grades.Uas)
			fmt.Printf("Input nilai Quiz untuk %s: ", matkul.Subject)
			fmt.Scan(&matkul.Grades.Quiz)
			matkul.Grades.Total = (matkul.Grades.Uts + matkul.Grades.Uas + matkul.Grades.Quiz) / 3
			matkul.Grades.Grade = calculateGrade(matkul.Grades.Total)
			
			(*students)[i].Matakuliah = append((*students)[i].Matakuliah, matkul)
			(*students)[i].Sks += 2
			totalNilai := 0.0
			for _, matkul := range (*students)[i].Matakuliah {
				totalNilai += matkul.Grades.Total
			}
			(*students)[i].Nilai = totalNilai / float64(len((*students)[i].Matakuliah))
			fmt.Println("Mata kuliah telah ditambahkan.")
			waitForKeypress()
			return
		}
	}
	fmt.Println("Mahasiswa dengan NIM tersebut tidak ditemukan!")
	waitForKeypress()
}

func deleteSubject(students *[]Mahasiswa) {
	var NIM string
	fmt.Printf("Masukkan NIM mahasiswa yang ingin diubah: ")
	fmt.Scan(&NIM)
	for i := range *students {
		if (*students)[i].Nim == NIM {
			fmt.Printf("Menghapus mata kuliah untuk %s\n", (*students)[i].Nama)

			fmt.Println("Daftar mata kuliah:")
			for j, matkul := range (*students)[i].Matakuliah {
				fmt.Printf("%d. %s\n", j+1, matkul.Subject)
			}

			var index int
			fmt.Printf("Pilih nomor mata kuliah yang ingin dihapus: ")
			fmt.Scan(&index)

			if index > 0 && index <= len((*students)[i].Matakuliah) {
				index--
				(*students)[i].Matakuliah = append((*students)[i].Matakuliah[:index], (*students)[i].Matakuliah[index+1:]...)
				(*students)[i].Sks -= 2
				fmt.Println("Mata kuliah telah dihapus.")
			} else {
				fmt.Println("Nomor mata kuliah tidak valid.")
			}
			totalNilai := 0.0
			for _, matkul := range (*students)[i].Matakuliah {
				totalNilai += matkul.Grades.Total
			}
			(*students)[i].Nilai = totalNilai / float64(len((*students)[i].Matakuliah))
			waitForKeypress()
			return
		}
	}
	fmt.Println("Mahasiswa dengan NIM tersebut tidak ditemukan!")
	waitForKeypress()
}

func displayStudentsBySubject(students []Mahasiswa) {
	scanner := bufio.NewScanner(os.Stdin)
	fmt.Printf("Masukkan nama mata kuliah: ")
	scanner.Scan()
	subject := scanner.Text()
	found := false
	i := 1
	fmt.Println("-------------------------------------------------")
	for _, student := range students {
		for _, matkul := range student.Matakuliah {
			if matkul.Subject == subject {
				fmt.Printf("%d. Nama: %s, NIM: %s\n", i, student.Nama, student.Nim)
				found = true
				i++
			}
		}
	}
	if !found {
		fmt.Println("Tidak ada mahasiswa yang mengambil mata kuliah tersebut.")
	}
	fmt.Println("-------------------------------------------------")
	waitForKeypress()
}

func displaySubjectsByStudent(students []Mahasiswa) {
	var NIM string
	fmt.Printf("Masukkan NIM mahasiswa: ")
	fmt.Scan(&NIM)
	found := false
	fmt.Println("-------------------------------------------------")
	for _, student := range students {
		if student.Nim == NIM {
			fmt.Printf("Nama: %s, NIM: %s\n", student.Nama, student.Nim)
			fmt.Println("Daftar Mata Kuliah:")
			for i, matkul := range student.Matakuliah {
				fmt.Printf("%d. %s\n", i+1, matkul.Subject)
			}
			found = true
		}
	}
	if !found {
		fmt.Println("Mahasiswa dengan NIM tersebut tidak ditemukan.")
	}
	fmt.Println("-------------------------------------------------")
	waitForKeypress()
}

func editData(students []Mahasiswa) {
	var NIM string
	fmt.Printf("Masukkan NIM mahasiswa yang ingin diubah: ")
	fmt.Scan(&NIM)
	for i := range students {
		if students[i].Nim == NIM {
			fmt.Printf("Mengubah data untuk %s\n", students[i].Nama)

			fmt.Println("Daftar mata kuliah:")
			for j, matkul := range students[i].Matakuliah {
				fmt.Printf("%d. %s\n", j+1, matkul.Subject)
			}

			var subjectIndex int
			fmt.Printf("Pilih nomor mata kuliah yang ingin diubah: ")
			fmt.Scan(&subjectIndex)

			if subjectIndex > 0 && subjectIndex <= len(students[i].Matakuliah) {
				subjectIndex--

				fmt.Printf("Input nilai UTS untuk %s: ", students[i].Matakuliah[subjectIndex].Subject)
				fmt.Scan(&students[i].Matakuliah[subjectIndex].Grades.Uts)
				fmt.Printf("Input nilai UAS untuk %s: ", students[i].Matakuliah[subjectIndex].Subject)
				fmt.Scan(&students[i].Matakuliah[subjectIndex].Grades.Uas)
				fmt.Printf("Input nilai Quiz untuk %s: ", students[i].Matakuliah[subjectIndex].Subject)
				fmt.Scan(&students[i].Matakuliah[subjectIndex].Grades.Quiz)

				students[i].Matakuliah[subjectIndex].Grades.Total = (students[i].Matakuliah[subjectIndex].Grades.Uts + students[i].Matakuliah[subjectIndex].Grades.Uas + students[i].Matakuliah[subjectIndex].Grades.Quiz) / 3
				students[i].Matakuliah[subjectIndex].Grades.Grade = calculateGrade(students[i].Matakuliah[subjectIndex].Grades.Total)

				fmt.Println("Data mata kuliah telah diubah.")
				totalNilai := 0.0
				for _, matkul := range students[i].Matakuliah {
					totalNilai += matkul.Grades.Total
				}
				students[i].Nilai = totalNilai / float64(len(students[i].Matakuliah))
			} else {
				fmt.Println("Nomor mata kuliah tidak valid.")
			}
			waitForKeypress()
			return
		}
	}
	fmt.Println("Mahasiswa dengan NIM tersebut tidak ditemukan!")
}

func inputData(students *[]Mahasiswa) {
	scanner := bufio.NewScanner(os.Stdin)
	var n int
	fmt.Printf("Input jumlah mahasiswa: ")
	fmt.Scan(&n)
	bufio.NewScanner(os.Stdin).Scan()
	for i := 0; i < n; i++ {
		var student Mahasiswa
		var subjectCount int
		fmt.Printf("Input Nama Mahasiswa #%d: ", i+1)
		scanner.Scan()
		student.Nama = scanner.Text()
		fmt.Printf("Input NIM: ")
		scanner.Scan()
		student.Nim = scanner.Text()
		fmt.Printf("Input jumlah mata kuliah untuk %s: ", student.Nama)
		fmt.Scan(&subjectCount)
		bufio.NewScanner(os.Stdin).Scan()
		student.Sks += subjectCount * 2
		totalNilai := 0.0
		for j := 0; j < subjectCount; j++ {
			var matkul Matakuliah
			fmt.Printf("Input nama mata kuliah #%d: ", j+1)
			scanner.Scan()
			matkul.Subject = scanner.Text()
			fmt.Printf("Input nilai UTS untuk %s: ", matkul.Subject)
			fmt.Scan(&matkul.Grades.Uts)
			bufio.NewScanner(os.Stdin).Scan()
			fmt.Printf("Input nilai UAS untuk %s: ", matkul.Subject)
			fmt.Scan(&matkul.Grades.Uas)
			bufio.NewScanner(os.Stdin).Scan()
			fmt.Printf("Input nilai Quiz untuk %s: ", matkul.Subject)
			fmt.Scan(&matkul.Grades.Quiz)
			bufio.NewScanner(os.Stdin).Scan()
			matkul.Grades.Total = (matkul.Grades.Uts + matkul.Grades.Uas + matkul.Grades.Quiz) / 3
			matkul.Grades.Grade = calculateGrade(matkul.Grades.Total)
			totalNilai += matkul.Grades.Total
			student.Matakuliah = append(student.Matakuliah, matkul)
		}
		student.Nilai = totalNilai / float64(subjectCount)
		*students = append(*students, student)
	}
}

func displayAll(students []Mahasiswa) {
	if len(students) == 0 {
		fmt.Println("Data Kosong!")
		return
	}
	for i, student := range students {
		fmt.Printf("=========================\n\n")
		fmt.Printf("Mahasiswa #%d:\n", i+1)
		fmt.Println("Nama:", student.Nama)
		fmt.Println("NIM:", student.Nim)
		fmt.Printf("Total SKS: %d\n", student.Sks)
		for _, matkul := range student.Matakuliah {
			fmt.Printf("Mata Kuliah: %s\n", matkul.Subject)
			fmt.Printf("Nilai UTS: %.2f\n", matkul.Grades.Uts)
			fmt.Printf("Nilai UAS: %.2f\n", matkul.Grades.Uas)
			fmt.Printf("Nilai Quiz: %.2f\n", matkul.Grades.Quiz)
			fmt.Printf("Total nilai: %.2f\n", matkul.Grades.Total)
			fmt.Printf("Grade: %s\n\n", matkul.Grades.Grade)
		}
	}
	fmt.Printf("=========================\n")
	waitForKeypress()
	
}

func calculateGrade(total float64) string {
	switch {
	case total >= 85:
		return "A"
	case total >= 70:
		return "B"
	case total >= 55:
		return "C"
	case total >= 40:
		return "D"
	default:
		return "E"
	}
}
