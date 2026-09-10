# edu-python-for-test


## Instructions

### Login to client

```bash
ssh -p 2223 dev@localhost   # password dev, respond yes if prompted about signature
```

### Basic Pet TestCase

```python
cat > tests/test_pets.py << 'EOF'
import unittest
import requests

class PetTestCase(unittest.TestCase):
    BASE_URL = "http://192.168.2.12:8080/api/v2"

    # test_create_pet
    # test_get_pet_by_id
    # test_update_pet
    # test_delete_pet
    # test_upload_pet_image
    # test_find_pets_by_status
    pass
EOF
```

### Hello World Test

```python
def test_should_be_equal_to_itself(self):
         # Given
         expected = "Hello World"

         # When
         actual = "Hello World"

         # Then
         self.assertEqual(expected,actual)
```

### Post (Create) Test

```python
# test_create_pet
     def test_should_be_able_to_create_pet(self):
         # Given
         payload = {
                 "id": 1,
                 "name": "Rocky",
                 "category": {"id": 1, "name": "cat"},
                 "status":"available"
                 }

         # When
         response = requests.post(f"{self.BASE_URL}/pet", json=payload)

         # Then
         self.assertEqual(200, response.status_code)
         self.assertEqual(payload["name"], response.json()["name"])
```

