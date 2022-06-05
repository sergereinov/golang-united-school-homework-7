package coverage

import (
	"math"
	"os"
	"reflect"
	"sort"
	"testing"
	"time"
)

// DO NOT EDIT THIS FUNCTION
func init() {
	content, err := os.ReadFile("students_test.go")
	if err != nil {
		panic(err)
	}
	err = os.WriteFile("autocode/students_test", content, 0644)
	if err != nil {
		panic(err)
	}
}

// WRITE YOUR CODE BELOW

func TestPeopleSort(t *testing.T) {
	now := time.Now()
	people := People{
		Person{"Aaa", "Aaa", now.AddDate(-24, 0, 0)},
		Person{"Bbb", "Aaa", now.AddDate(-24, 0, 0)},
		Person{"Aaa", "Ccc", now.AddDate(-24, 0, 0)},
		Person{"Aaa", "Aaa", now.AddDate(-23, 0, 0)},
	}

	expect := People{
		Person{"Aaa", "Aaa", now.AddDate(-23, 0, 0)},
		Person{"Aaa", "Aaa", now.AddDate(-24, 0, 0)},
		Person{"Aaa", "Ccc", now.AddDate(-24, 0, 0)},
		Person{"Bbb", "Aaa", now.AddDate(-24, 0, 0)},
	}

	sort.Sort(people)

	if !reflect.DeepEqual(people, expect) {
		t.Fatalf("sort fail, got %v", people)
	}
}

func TestMatrixCreationErrors(t *testing.T) {

	corruptedCases := []string{
		"1 2\n3",
		"x",
	}

	for _, str := range corruptedCases {
		t.Run("case_"+str, func(t *testing.T) {
			if m, err := New(str); err == nil {
				t.Fatalf("there should be an error, but got %v", m)
			}
		})
	}
}

func TestMatrixCommon(t *testing.T) {
	expectMatrix := &Matrix{2, 2, []int{1, 2, 3, 4}}
	expectRows := [][]int{{1, 2}, {3, 4}}
	expectCols := [][]int{{1, 3}, {2, 4}}

	input := "1 2\n3 4"
	m, err := New(input)
	if err != nil {
		t.Fatalf("case %v got error %v", input, err)
	}

	if !reflect.DeepEqual(expectMatrix, m) {
		t.Fatalf("wrong matrix, want %v, but got %v", expectMatrix, m)
	}

	if r := m.Rows(); !reflect.DeepEqual(expectRows, r) {
		t.Fatalf("wrong rows, want %v, but got %v", expectRows, r)
	}

	if c := m.Cols(); !reflect.DeepEqual(expectCols, c) {
		t.Fatalf("wrong cols, want %v, but got %v", expectCols, c)
	}
}

func TestMatrixSet(t *testing.T) {

	testCases := map[string]struct {
		row, col, value int
		good            bool
	}{
		"good case":    {0, 0, 0, true},
		"negative row": {-1, 0, 0, false},
		"negative col": {0, -1, 0, false},
		"big row":      {math.MaxInt32, 0, 0, false},
		"big col":      {0, math.MaxInt32, 0, false},
	}

	input := "1 2\n3 4"

	for name, tc := range testCases {
		t.Run(name, func(t *testing.T) {
			m, _ := New(input)
			if tc.good != m.Set(tc.row, tc.col, tc.value) {
				t.Fatalf("fail set with %v on %v", tc, m)
			}

			if tc.good && tc.value != m.Rows()[tc.row][tc.col] {
				t.Fatalf("wrong value after set with %v, got m=%v", tc, m)
			}
		})
	}
}
