package coverage

import (
	"os"
	"reflect"
	"testing"
	"time"

	"github.com/google/go-cmp/cmp"
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

func TestLenPeople(t *testing.T) {
	ppl := People{
		{
			firstName: "sunbula",
			lastName:  "khasanova",
			birthDay:  time.Now(),
		},
		{
			firstName: "sunbula",
			lastName:  "khasanova",
			birthDay:  time.Now(),
		},
		{
			firstName: "sunbula",
			lastName:  "khasanova",
			birthDay:  time.Now(),
		},
	}

	got := ppl.Len()
	want := 3
	if got != want {
		t.Errorf("People.Len() failed got: %v, want: %v", got, want)
	}
}

func TestLessPeople(t *testing.T) {

	st, err := time.Parse("2006-02-01 15:04:05 -0700", "2010-23-07 00:00:00 +0000")
	if err != nil {
		t.Errorf("problem with parsing time: %v", err)
	}
	dt, _ := time.Parse("2006-02-01 15:04:05 -0700", "2000-21-07 00:00:00 +0000")
	if err != nil {
		t.Errorf("problem with parsing time: %v", err)
	}

	temp := People{
		{ //0
			firstName: "sunbula",
			lastName:  "khasanova",
			birthDay:  st,
		},
		{ //1
			firstName: "dildora",
			lastName:  "eshmurodova",
			birthDay:  dt,
		},
		{ //2
			firstName: "shaxnoza",
			lastName:  "soburova",
			birthDay:  dt,
		},
		{ // 3
			firstName: "shaxnoza",
			lastName:  "soburov",
			birthDay:  dt,
		},
		{ // 4

			firstName: "dildoraxon",
			lastName:  "eshmurodova",
			birthDay:  dt,
		},
		{ // 5
			firstName: "shaxnoza",
			lastName:  "soburovna",
			birthDay:  dt,
		},
	}

	data := []struct {
		name string
		ppl  People
		i, j int
		want bool
	}{
		{
			name: "p[i].firstName < p[j].firstName = true",
			ppl:  temp,
			i:    1,
			j:    2,
			want: true,
		},

		{
			name: "p[i].firstName < p[j].firstName = false",
			ppl:  temp,
			i:    2,
			j:    1,
			want: false,
		},
		{
			name: "p[i].lastName < p[j].lastName = true",
			ppl:  temp,
			i:    3,
			j:    5,
			want: true,
		},
		{
			name: "p[i].lastName < p[j].lastName = false",
			ppl:  temp,
			i:    5,
			j:    3,
			want: false,
		},
		{
			name: "p[i].birthDay.Unix() > p[j].birthDay.Unix() = false",
			ppl:  temp,
			i:    1,
			j:    0,
			want: false,
		},
		{
			name: "p[i].birthDay.Unix() > p[j].birthDay.Unix() = true",
			ppl:  temp,
			i:    0,
			j:    1,
			want: true,
		},
	}

	for _, d := range data {
		t.Run(d.name, func(t *testing.T) {
			got := temp.Less(d.i, d.j)
			if got != d.want {
				t.Errorf("People.Less() failed got: %v, want: %v", got, d.want)
			}
		})
	}

}

func TestSwapPeople(t *testing.T) {
	st, _ := time.Parse("2006-02-01 15:04:05 -0700", "2002-23-07 00:00:00 +0000")
	dt, _ := time.Parse("2006-02-01 15:04:05 -0700", "2000-21-07 00:00:00 +0000")
	sht, _ := time.Parse("2006-02-01 15:04:05 -0700", "2000-21-07 00:00:00 +0000")

	temp := People{
		{ //0
			firstName: "sunbula",
			lastName:  "khasanova",
			birthDay:  st,
		},
		{ //1
			firstName: "dildora",
			lastName:  "eshmurodova",
			birthDay:  dt,
		},
		{ //2
			firstName: "shaxnoza",
			lastName:  "soburova",
			birthDay:  sht,
		},
		{ // 3
			firstName: "shaxnoza",
			lastName:  "soburov",
			birthDay:  sht,
		},
		{ // 4

			firstName: "dildoraxon",
			lastName:  "eshmurodova",
			birthDay:  dt,
		},
		{ // 5
			firstName: "shaxnoza",
			lastName:  "soburovna",
			birthDay:  sht,
		},
	}
	want1 := temp[1]
	want2 := temp[0]

	temp.Swap(0, 1)
	got1 := temp[0]
	got2 := temp[1]

	opt := cmp.AllowUnexported(temp[0], temp[1])

	if diff := cmp.Diff(want2, got2, opt); diff != "" {
		t.Errorf("People.Swap() failed got: %v, want: %v", got2, want2)
	}
	if diff := cmp.Diff(want1, got1, opt); diff != "" {
		t.Errorf("People.Swap() failed got: %v, want: %v", got1, want1)
	}
}

func TestNewMatrix(t *testing.T) {

	data := []struct {
		name   string
		str    string
		want   *Matrix
		errMsg string
	}{
		{
			name: "successful return",
			str:  "1 1 1 \n 2 2 2 \n 3 3 3",
			want: &Matrix{
				rows: 3,
				cols: 3,
				data: []int{1, 1, 1, 2, 2, 2, 3, 3, 3},
			},
			errMsg: "",
		},
		{
			name:   "Rows needto be the same length",
			str:    "1 1 1 \n 2 2 ",
			want:   nil,
			errMsg: "Rows need to be the same length",
		},
		{
			name:   "not a number",
			str:    "1 1 l \n 2 2 2 \n 3 3 3",
			want:   nil,
			errMsg: "strconv.Atoi: parsing \"l\": invalid syntax",
		},
	}

	for _, d := range data {
		t.Run(d.name, func(t *testing.T) {
			got, err := New(d.str)
			comparer := cmp.Comparer(func(x, y Matrix) bool {
				slc := reflect.DeepEqual(x.data, y.data)
				return x.cols == y.cols && x.rows == x.rows && slc
			})

			if diff := cmp.Diff(got, d.want, comparer); diff != "" {
				t.Errorf("Expected %d, got %d", d.want, got)
			}
			var errMsg string
			if err != nil {
				errMsg = err.Error()
			}
			if errMsg != d.errMsg {
				t.Errorf("Expected error message `%s`, got `%s`",
					d.errMsg, errMsg)
			}

		})
	}

}

func TestRowsMatrix(t *testing.T) {
	str := "1 1 1 \n 2 2 2 \n 3 3 3"
	mtrx, err := New(str)
	if err != nil {
		t.Errorf("unexpected err: %v", err)
	}
	got := mtrx.Rows()
	want := [][]int{
		{1, 1, 1},
		{2, 2, 2},
		{3, 3, 3},
	}
	if diff := cmp.Diff(got, want); diff != "" {
		t.Errorf("want: %v, got: %v", want, got)
	}
}

func TestColsMatrix(t *testing.T) {
	str := "1 1 1 \n 2 2 2 \n 3 3 3"
	mtrx, err := New(str)
	if err != nil {
		t.Errorf("unexpected err: %v", err)
	}
	got := mtrx.Cols()
	want := [][]int{
		{1, 2, 3},
		{1, 2, 3},
		{1, 2, 3},
	}
	if diff := cmp.Diff(got, want); diff != "" {
		t.Errorf("want: %v, got: %v", want, got)
	}
}

func TestSetMatrix(t *testing.T) {
	str := "1 1 1 \n 2 2 2 \n 3 3 3"
	mtrx, err := New(str)
	if err != nil {
		t.Errorf("unexpected err: %v", err)
	}

	got := mtrx.Set(0, 0, 5)
	want := true
	if got != want {
		t.Errorf("want: %v, got: %v", want, got)
	}

	got = mtrx.Set(4, 4, 6)
	want = false
	if got != want {
		t.Errorf("want: %v, got: %v", want, got)
	}

}
