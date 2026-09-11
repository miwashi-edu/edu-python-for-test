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

### Get (Read) Test

```python
# test_get_pet_by_id
    def test_should_be_able_to_get_pet_by_id(self):
        # Given
        payload = {
            "id": 1,
            "name": "Rocky",
            "category": {"id": 1, "name": "cat"},
            "status": "available"
        }
        requests.post(f"{self.BASE_URL}/pet", json=payload)

        # When
        response = requests.get(f"{self.BASE_URL}/pet/{payload['id']}")

        # Then
        self.assertEqual(200, response.status_code)
        self.assertEqual(payload["id"], response.json()["id"])
        self.assertEqual(payload["name"], response.json()["name"])
```

### Put (Update) Test

```python
# test_update_pet
    def test_should_be_able_to_update_pet(self):
        # Given
        payload = {
            "id": 1,
            "name": "Rocky",
            "category": {"id": 1, "name": "cat"},
            "status": "available"
        }
        requests.post(f"{self.BASE_URL}/pet", json=payload)
        updated_payload = dict(payload, name="Rocky Updated", status="sold")

        # When
        response = requests.put(f"{self.BASE_URL}/pet", json=updated_payload)

        # Then
        self.assertEqual(200, response.status_code)
        self.assertEqual("Rocky Updated", response.json()["name"])
        self.assertEqual("sold", response.json()["status"])
```

### Delete (Delete) Test

```python
# test_delete_pet
    def test_should_be_able_to_delete_pet(self):
        # Given
        payload = {
            "id": 1,
            "name": "Rocky",
            "category": {"id": 1, "name": "cat"},
            "status": "available"
        }
        requests.post(f"{self.BASE_URL}/pet", json=payload)

        # When
        response = requests.delete(f"{self.BASE_URL}/pet/{payload['id']}")

        # Then
        self.assertEqual(200, response.status_code)
        get_response = requests.get(f"{self.BASE_URL}/pet/{payload['id']}")
        self.assertEqual(404, get_response.status_code)
```

### Upload Image

> Observe photo.jpg, must exist!

```python
# test_upload_pet_image
    def test_should_be_able_to_upload_pet_image(self):
        # Given
        payload = {
            "id": 1,
            "name": "Rocky",
            "category": {"id": 1, "name": "cat"},
            "status": "available"
        }
        requests.post(f"{self.BASE_URL}/pet", json=payload)
        files = {"file": ("photo.jpg", b"fake-image-bytes", "image/jpeg")}

        # When
        response = requests.post(f"{self.BASE_URL}/pet/{payload['id']}/uploadImage", files=files)

        # Then
        self.assertEqual(200, response.status_code)
```



