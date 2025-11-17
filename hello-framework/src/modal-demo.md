# Modal Demo

This page demonstrates a simple, reusable modal implementation.

## Demo

```js echo
const openModalBtn = view(Inputs.button("Open Modal", {reduce: () => showModal()}));
```

<div id="modal-container"></div>

---

## Implementation

### JavaScript: Modal State Management

```js echo
// Modal state
const modalState = Mutable({isOpen: false});

// Show modal function
function showModal() {
  modalState.value = {isOpen: true};
}

// Hide modal function
function hideModal() {
  modalState.value = {isOpen: false};
}
```

### JavaScript: Reactive Modal Rendering

```js echo
// Reactive modal rendering
{
  const container = document.querySelector('#modal-container');

  if (modalState.isOpen) {
    container.innerHTML = `
      <div class="modal-overlay" id="modal-overlay">
        <div class="modal-dialog">
          <div class="modal-header">
            <h2 class="modal-title">Demo Modal</h2>
            <button class="modal-close" id="modal-close" aria-label="Close">&times;</button>
          </div>
          <div class="modal-body">
            <p>This is a demo modal dialog. You can put any content here:</p>
            <ul>
              <li>Forms</li>
              <li>Images</li>
              <li>Charts</li>
              <li>Any HTML content</li>
            </ul>
            <p>Click the X button, press Escape, or click outside the modal to close it.</p>
          </div>
          <div class="modal-footer">
            <button class="btn-secondary" id="modal-cancel">Cancel</button>
            <button class="btn-primary" id="modal-confirm">Confirm</button>
          </div>
        </div>
      </div>
    `;

    // Add event listeners
    document.getElementById('modal-overlay').addEventListener('click', (e) => {
      if (e.target.id === 'modal-overlay') {
        hideModal();
      }
    });

    document.getElementById('modal-close').addEventListener('click', hideModal);
    document.getElementById('modal-cancel').addEventListener('click', hideModal);
    document.getElementById('modal-confirm').addEventListener('click', () => {
      alert('Confirmed!');
      hideModal();
    });

    // Keyboard support
    const handleEscape = (e) => {
      if (e.key === 'Escape') {
        hideModal();
        document.removeEventListener('keydown', handleEscape);
      }
    };
    document.addEventListener('keydown', handleEscape);

    // Focus trap
    document.getElementById('modal-close').focus();
  } else {
    container.innerHTML = '';
  }
}
```

### CSS: Modal Styles

```html echo
<style>
  .modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    background-color: rgba(0, 0, 0, 0.5);
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 1000;
    animation: fadeIn 0.2s ease-out;
  }

  @keyframes fadeIn {
    from {
      opacity: 0;
    }
    to {
      opacity: 1;
    }
  }

  .modal-dialog {
    background: white;
    border-radius: 8px;
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1), 0 10px 20px rgba(0, 0, 0, 0.15);
    max-width: 500px;
    width: 90%;
    max-height: 90vh;
    display: flex;
    flex-direction: column;
    animation: slideIn 0.2s ease-out;
  }

  @keyframes slideIn {
    from {
      transform: translateY(-20px);
      opacity: 0;
    }
    to {
      transform: translateY(0);
      opacity: 1;
    }
  }

  .modal-header {
    padding: 1.5rem;
    border-bottom: 1px solid #e5e7eb;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }

  .modal-title {
    margin: 0;
    font-size: 1.25rem;
    font-weight: 600;
    color: #111827;
  }

  .modal-close {
    background: none;
    border: none;
    font-size: 1.5rem;
    line-height: 1;
    color: #6b7280;
    cursor: pointer;
    padding: 0;
    width: 2rem;
    height: 2rem;
    display: flex;
    align-items: center;
    justify-content: center;
    border-radius: 4px;
    transition: background-color 0.2s, color 0.2s;
  }

  .modal-close:hover {
    background-color: #f3f4f6;
    color: #111827;
  }

  .modal-body {
    padding: 1.5rem;
    overflow-y: auto;
    color: #374151;
  }

  .modal-footer {
    padding: 1.5rem;
    border-top: 1px solid #e5e7eb;
    display: flex;
    gap: 0.75rem;
    justify-content: flex-end;
  }

  .btn-primary,
  .btn-secondary {
    padding: 0.5rem 1rem;
    border-radius: 6px;
    font-weight: 500;
    cursor: pointer;
    border: 1px solid transparent;
    transition: all 0.2s;
  }

  .btn-primary {
    background-color: #3b82f6;
    color: white;
  }

  .btn-primary:hover {
    background-color: #2563eb;
  }

  .btn-secondary {
    background-color: white;
    color: #374151;
    border-color: #d1d5db;
  }

  .btn-secondary:hover {
    background-color: #f9fafb;
  }
</style>
```

### HTML: Modal Container

The modal is injected into this container element:

```html echo
<div id="modal-container"></div>
```

---

## Features

This modal implementation includes:

- **Overlay backdrop** - Semi-transparent background that dims the page
- **Click outside to close** - Clicking the overlay closes the modal
- **Escape key support** - Press Escape to close
- **Close button** - X button in the header
- **Action buttons** - Cancel and Confirm buttons in the footer
- **Smooth animations** - Fade in overlay and slide in dialog
- **Responsive design** - Works on mobile and desktop
- **Accessibility** - Focus management and keyboard support

## Usage

Click the "Open Modal" button at the top of the page to see it in action!
