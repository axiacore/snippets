# Python snippets


### Generating a test image

Generate a test image for test usage

```python
from io import BytesIO
from PIL import Image

from django.core.files.uploadedfile import InMemoryUploadedFile


def get_test_image():
    """Returns an image for running tests
    """
    io_var = BytesIO()
    size = (10, 10)
    color = (255, 0, 0, 0)

    image = Image.new('RGBA', size, color)
    image.save(io_var, format='JPEG')
    image_file = InMemoryUploadedFile(
        io_var,
        None,
        'test.jpg',
        'jpeg',
        None,
        None
    )
    image_file.seek(0)

    return image_file
```

### Making all model fields readonly in the admin


```python
def get_readonly_fields(self, request, obj=None):
    if obj is None:
        return super(
            ModelName,
            self
        ).get_readonly_fields(
            request,
            obj,
        )
    # Make all fields readonly.
    read_only_fields = list(set(
        [field.name for field in self.opts.local_fields] +
        [field.name for field in self.opts.local_many_to_many]
    ))
    return read_only_fields
```
