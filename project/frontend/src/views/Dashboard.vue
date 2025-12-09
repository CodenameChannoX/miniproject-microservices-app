<template>
  <div class="dashboard">
    <nav class="navbar">
      <div class="nav-left">
        <h1>Microservices Dashboard</h1>
      </div>
      <div class="nav-right">
        <span>Welcome, {{ user.name }}</span>
        <button @click="handleLogout" class="btn-logout">Logout</button>
      </div>
    </nav>
    
    <div class="main-content">
      <div class="sidebar">
        <h3>Services</h3>
        <ul>
          <li><router-link to="/products">Products</router-link></li>
          <li><router-link to="/users">Users</router-link></li>
          <li><router-link to="/analytics">Analytics</router-link></li>
        </ul>
      </div>
      
      <div class="content">
        <h2>System Architecture</h2>
        <div class="architecture-diagram">
          <div class="service-card">
            <h4>Vue.js Frontend</h4>
            <p>Port: 8080</p>
          </div>
          <div class="arrow">→</div>
          <div class="service-card">
            <h4>Auth Service</h4>
            <p>Node.js + PostgreSQL</p>
            <p>Port: 3001</p>
          </div>
          <div class="arrow">→</div>
          <div class="service-card">
            <h4>Product Service</h4>
            <p>Node.js + MongoDB</p>
            <p>Port: 3002</p>
          </div>
        </div>
        
        <div class="stats">
          <div class="stat-card">
            <h4>PostgreSQL</h4>
            <p>Port: 5432</p>
            <p>Users Database</p>
          </div>
          <div class="stat-card">
            <h4>MongoDB</h4>
            <p>Port: 27017</p>
            <p>Products Database</p>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'Dashboard',
  data() {
    return {
      user: JSON.parse(localStorage.getItem('user') || '{}')
    };
  },
  methods: {
    handleLogout() {
      localStorage.removeItem('token');
      localStorage.removeItem('user');
      this.$router.push('/login');
    }
  }
};
</script>

<style scoped>
.dashboard {
  min-height: 100vh;
  background: #f7fafc;
}

.navbar {
  background: white;
  padding: 1rem 2rem;
  display: flex;
  justify-content: space-between;
  align-items: center;
  box-shadow: 0 2px 4px rgba(0,0,0,0.1);
}

.nav-right {
  display: flex;
  align-items: center;
  gap: 1rem;
}

.btn-logout {
  padding: 0.5rem 1rem;
  background: #e53e3e;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.main-content {
  display: flex;
  min-height: calc(100vh - 70px);
}

.sidebar {
  width: 250px;
  background: #2d3748;
  color: white;
  padding: 2rem;
}

.sidebar ul {
  list-style: none;
  padding: 0;
}

.sidebar li {
  margin: 1rem 0;
}

.sidebar a {
  color: #cbd5e0;
  text-decoration: none;
}

.sidebar a:hover {
  color: white;
}

.content {
  flex: 1;
  padding: 2rem;
}

.architecture-diagram {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 2rem;
  margin: 3rem 0;
  flex-wrap: wrap;
}

.service-card {
  background: white;
  padding: 1.5rem;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0,0,0,0.1);
  text-align: center;
  min-width: 200px;
}

.arrow {
  font-size: 2rem;
  color: #718096;
}

.stats {
  display: flex;
  gap: 2rem;
  margin-top: 3rem;
}

.stat-card {
  background: white;
  padding: 1.5rem;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0,0,0,0.1);
  flex: 1;
}
</style>
