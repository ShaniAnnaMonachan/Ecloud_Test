users=[]

# Create User

def create1():
    new_user = {
        'username': request.json['username'],
        'password': request.json['password'],
        'active': request.json.get('active', True)  
    }
    users.append(new_user)
    return jsonify(new_user)

# Read User

def read2(username):
    user = find_user(username)
    if user is None:
        return jsonify({'error': 'User not found'})
    return jsonify(user)

# Update User

def update3(username):
    user = find_user(username)
    if user is None:
        return jsonify({'error': 'User not found'})
    user['password'] = request.json.get('password', user['password'])
    user['active'] = request.json.get('active', user['active'])
    return jsonify(user)

# Delete a user

def delete4(username):
    user = find_user(username)
    if user is None:
        return jsonify({'error': 'User not found'})
    users.remove(user)
    return jsonify({'message': 'User deleted'})
