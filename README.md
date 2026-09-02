# edu-python-for-test


## Instructions

### Prepare
```
cd ~
cd ws
cd edu-python-for-test
git pull
docker compose down
docker compose up -d
docker ps
```

### Petstore Open API 3.0

[http://localhost:8080](http://localhost:8080)

### Login to client

```bash
ssh -p 2223 dev@localhost   # password dev, respond yes if prompted about signature
```

### Prepare

```bash
cd ~
mkdir ws
cd ws
mkdir tests && cd tests
```

### Create Scripts

```bash
cat > test_all << 'EOF'
#!/usr/bin/env python3
import unittest

from tests.test_pets import PetTestCase
from tests.test_store import StoreTestCase
from tests.test_orders import OrderTestCase
from tests.test_inventory import InventoryTestCase
from tests.test_users import UserTestCase

def suite():
    suite = unittest.TestSuite()
    suite.addTests(unittest.TestLoader().loadTestsFromTestCase(PetTestCase))
    suite.addTests(unittest.TestLoader().loadTestsFromTestCase(StoreTestCase))
    suite.addTests(unittest.TestLoader().loadTestsFromTestCase(OrderTestCase))
    suite.addTests(unittest.TestLoader().loadTestsFromTestCase(InventoryTestCase))
    suite.addTests(unittest.TestLoader().loadTestsFromTestCase(UserTestCase))
    return suite

if __name__ == "__main__":
    runner = unittest.TextTestRunner(verbosity=2)
    runner.run(suite())
EOF

mkdir -p tests

cat > tests/__init__.py << 'EOF'
EOF

cat > tests/test_pets.py << 'EOF'
import unittest

class PetTestCase(unittest.TestCase):
    # test_create_pet
    # test_get_pet_by_id
    # test_update_pet
    # test_delete_pet
    # test_upload_pet_image
    # test_find_pets_by_status
    pass
EOF

cat > tests/test_store.py << 'EOF'
import unittest

class StoreTestCase(unittest.TestCase):
    # test_get_inventory
    # test_place_order
    pass
EOF

cat > tests/test_orders.py << 'EOF'
import unittest

class OrderTestCase(unittest.TestCase):
    # test_get_order_by_id
    # test_delete_order
    # test_place_order_invalid_id
    pass
EOF

cat > tests/test_inventory.py << 'EOF'
import unittest

class InventoryTestCase(unittest.TestCase):
    # test_inventory_status_counts
    pass
EOF

cat > tests/test_users.py << 'EOF'
import unittest

class UserTestCase(unittest.TestCase):
    # test_create_user
    # test_login_user
    # test_logout_user
    # test_get_user_by_username
    # test_update_user
    # test_delete_user
    pass
EOF

chmod +x test_all
```



### Generate new signatures if needed

> When you see  
> @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@  
> @    WARNING: REMOTE HOST IDENTIFICATION HAS CHANGED!     @  
> @@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@  

```bash
ssh-keygen -R "[localhost]:2222" # Add new key if needed 
ssh-keygen -R "[localhost]:2223" # Add new key if needed
cat ~/.ssh/known_hosts # Optional, this is where the keys are stored (can be edited in vim also)
cat ~/.ssh/known_hosts | grep 2222 # Filter output
cat ~/.ssh/known_hosts | grep 2223 # Filter output
```




