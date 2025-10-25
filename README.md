# app-notes

import React, { useState, useEffect } from 'react';

function App() {
  const [notes, setNotes] = useState(() => {
    const saved = localStorage.getItem('notes');
    return saved ? JSON.parse(saved) : [];
  });
  const [input, setInput] = useState('');

  useEffect(() => {
    localStorage.setItem('notes', JSON.stringify(notes));
  }, [notes]);

  const addNote = () => {
    if (input.trim() === '') return;
    setNotes([...notes, input]);
    setInput('');
  };

  const deleteNote = (index) => {
    const newNotes = notes.filter((_, i) => i !== index);
    setNotes(newNotes);
  };

  return (
    <div style={{ padding: 20, maxWidth: 500, margin: 'auto' }}>
      <h1>📝 یادداشت‌های من</h1>
      <div style={{ display: 'flex', gap: 10 }}>
        <input
          type="text"
          value={input}
          onChange={(e) => setInput(e.target.value)}
          placeholder="یادداشت جدید..."
          style={{ flex: 1, padding: 8 }}
        />
        <button onClick={addNote}>افزودن</button>
      </div>
      <ul style={{ marginTop: 20, padding: 0, listStyle: 'none' }}>
        {notes.map((note, index) => (
          <li key={index} style={{ background: '#eee', padding: 10, marginBottom: 8, display: 'flex', justifyContent: 'space-between' }}>
            {note}
            <button onClick={() => deleteNote(index)}>🗑️</button>
          </li>
        ))}
      </ul>
    </div>
  );
}

export default App;
