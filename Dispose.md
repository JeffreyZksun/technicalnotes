# Dispose #
The Dispose method is the implemented of Dispose design pattern.`[1]`

Then framework doesn't guarantee when the destructor is called. If the class encapsulate the expensive unmanged resources and they are requied to be released as early as possible, the Dispose method plays a role in this case.

A Dispose method should call the SuppressFinalize method for the object it is disposing.

```
public class DisposableResource : IDisposable
{

    private Stream _resource;  
    private bool _disposed;

    // The stream passed to the constructor 
    // must be readable and not null.
    public DisposableResource(Stream stream)
    {
        if (stream == null)
            throw new ArgumentNullException("Stream in null.");
        if (!stream.CanRead)
            throw new ArgumentException("Stream must be readable.");

        _resource = stream;

        _disposed = false;
    }

    // Demonstrates using the resource. 
    // It must not be already disposed.
    public void DoSomethingWithResource() {
        if (_disposed)
            throw new ObjectDisposedException("Resource was disposed.");

        // Show the number of bytes.
        int numBytes = (int) _resource.Length;
        Console.WriteLine("Number of bytes: {0}", numBytes.ToString());
    }


    public void Dispose() 
    {
        Dispose(true);

        // Use SupressFinalize in case a subclass
        // of this type implements a finalizer.
        GC.SuppressFinalize(this);      
    }

    protected virtual void Dispose(bool disposing)
    {
        // If you need thread safety, use a lock around these 
        // operations, as well as in your methods that use the resource.
        if (!_disposed)
        {
            if (disposing) {
                if (_resource != null)
                    _resource.Dispose();
                    Console.WriteLine("Object disposed.");
            }

            // Indicate that the instance has been disposed.
            _resource = null;
            _disposed = true;   
        }
    }
}
```

> # Reference #
`[1]` http://msdn.microsoft.com/en-us/library/fs2xkftw%28v=vs.110%29.aspx