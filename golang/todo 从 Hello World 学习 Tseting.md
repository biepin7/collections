## Hello World

```go
package greeting

// HelloWorld greets the world.
func HelloWorld() string {
	return "Hello, World!"
}

```

## Testing

```go
package greeting
import "testing"

func TestHelloWorld(t *testing.T) {
	expected := "Hello, World!"
	if observed := HelloWorld(); observed != expected {
		t.Fatalf("HelloWorld() = %v, want %v", observed, expected)
	}
}

func BenchmarkHelloWorld(b *testing.B) {
	if testing.Short() {
		b.Skip("skipping benchmark in short mode.")
	}
	for i := 0; i < b.N; i++ {
		HelloWorld()
	}
}
```

