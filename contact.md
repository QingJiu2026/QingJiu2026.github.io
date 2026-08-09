---
layout: default
title: Contact
permalink: /contact/
---

# Get in Touch

Have questions or want to reach out? Fill out the form below and I'll get back to you as soon as possible.

<form id="contactForm" class="contact-form">
  <div class="form-group">
    <label for="name">Name</label>
    <input type="text" id="name" name="name" required>
  </div>

  <div class="form-group">
    <label for="email">Email</label>
    <input type="email" id="email" name="email" required>
  </div>

  <div class="form-group">
    <label for="subject">Subject</label>
    <input type="text" id="subject" name="subject" required>
  </div>

  <div class="form-group">
    <label for="message">Message</label>
    <textarea id="message" name="message" rows="5" required></textarea>
  </div>

  <button type="submit" class="btn-submit">Send Message</button>
  <div id="formMessage" class="form-message"></div>
</form>

<style>
  .contact-form {
    max-width: 600px;
    margin: 30px auto;
    padding: 20px;
    background-color: #f9f9f9;
    border-radius: 8px;
    box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
  }

  .form-group {
    margin-bottom: 20px;
    display: flex;
    flex-direction: column;
  }

  .contact-form label {
    margin-bottom: 8px;
    font-weight: bold;
    color: #333;
  }

  .contact-form input,
  .contact-form textarea {
    padding: 10px;
    border: 1px solid #ddd;
    border-radius: 4px;
    font-family: Arial, sans-serif;
    font-size: 14px;
  }

  .contact-form input:focus,
  .contact-form textarea:focus {
    outline: none;
    border-color: #007bff;
    box-shadow: 0 0 5px rgba(0, 123, 255, 0.3);
  }

  .btn-submit {
    padding: 12px 30px;
    background-color: #007bff;
    color: white;
    border: none;
    border-radius: 4px;
    cursor: pointer;
    font-size: 16px;
    font-weight: bold;
    transition: background-color 0.3s;
  }

  .btn-submit:hover {
    background-color: #0056b3;
  }

  .btn-submit:active {
    background-color: #004494;
  }

  .form-message {
    margin-top: 15px;
    padding: 12px;
    border-radius: 4px;
    text-align: center;
    display: none;
  }

  .form-message.success {
    display: block;
    background-color: #d4edda;
    color: #155724;
    border: 1px solid #c3e6cb;
  }

  .form-message.error {
    display: block;
    background-color: #f8d7da;
    color: #721c24;
    border: 1px solid #f5c6cb;
  }
</style>

<script>
  document.getElementById('contactForm').addEventListener('submit', async function(e) {
    e.preventDefault();
    
    const formMessage = document.getElementById('formMessage');
    formMessage.innerHTML = '';
    
    // Get form data
    const formData = {
      name: document.getElementById('name').value,
      email: document.getElementById('email').value,
      subject: document.getElementById('subject').value,
      message: document.getElementById('message').value,
      timestamp: new Date().toISOString()
    };
    
    try {
      // Store in localStorage as a simple solution (no backend required)
      const existingMessages = JSON.parse(localStorage.getItem('contactMessages') || '[]');
      existingMessages.push(formData);
      localStorage.setItem('contactMessages', JSON.stringify(existingMessages));
      
      // Show success message
      formMessage.className = 'form-message success';
      formMessage.innerHTML = '✓ Thank you for your message! I\'ll get back to you soon.';
      
      // Reset form
      document.getElementById('contactForm').reset();
      
      // Clear message after 5 seconds
      setTimeout(() => {
        formMessage.innerHTML = '';
      }, 5000);
    } catch (error) {
      // Show error message
      formMessage.className = 'form-message error';
      formMessage.innerHTML = '✗ There was an error sending your message. Please try again.';
    }
  });
</script>
