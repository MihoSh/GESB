const express = require('express');
const mongoose = require('mongoose');
const bodyParser = require('body-parser');

const app = express();
const PORT = 3000;

// Middleware
app.use(bodyParser.json());
app.use(bodyParser.urlencoded({ extended: true }));

// MongoDB Connection
mongoose.connect('mongodb://localhost:27017/gaming-tournaments', { useNewUrlParser: true, useUnifiedTopology: true })
    .then(() => console.log('MongoDB connected'))
    .catch(err => console.error(err));

// Schemas
const userSchema = new mongoose.Schema({
    username: { type: String, required: true },
    email: { type: String, required: true },
    password: { type: String, required: true }
});

const tournamentSchema = new mongoose.Schema({
    game: { type: String, required: true },
    details: { type: String, required: true },
    date: { type: Date, required: true }
});

const newsSchema = new mongoose.Schema({
    title: { type: String, required: true },
    content: { type: String, required: true },
    date: { type: Date, default: Date.now }
});

const contactSchema = new mongoose.Schema({
    name: { type: String, required: true },
    email: { type: String, required: true },
    message: { type: String, required: true },
    date: { type: Date, default: Date.now }
});

const collaborationSchema = new mongoose.Schema({
    name: { type: String, required: true },
    email: { type: String, required: true },
    proposal: { type: String, required: true },
    date: { type: Date, default: Date.now }
});

// Models
const User = mongoose.model('User', userSchema);
const Tournament = mongoose.model('Tournament', tournamentSchema);
const News = mongoose.model('News', newsSchema);
const Contact = mongoose.model('Contact', contactSchema);
const Collaboration = mongoose.model('Collaboration', collaborationSchema);

// Routes
app.get('/', (req, res) => {
    res.send('Welcome to the Gaming Tournaments API');
});

app.post('/create-account', (req, res) => {
    const { username, email, password } = req.body;
    
    const newUser = new User({ username, email, password });
    
    newUser.save()
        .then(user => res.status(201).json(user))
        .catch(err => res.status(400).json({ error: err.message }));
});

app.post('/add-tournament', (req, res) => {
    const { game, details, date } = req.body;
    
    const newTournament = new Tournament({ game, details, date });
    
    newTournament.save()
        .then(tournament => res.status(201).json(tournament))
        .catch(err => res.status(400).json({ error: err.message }));
});

app.get('/tournaments', (req, res) => {
    Tournament.find()
        .then(tournaments => res.json(tournaments))
        .catch(err => res.status(400).json({ error: err.message }));
});

app.post('/add-news', (req, res) => {
    const { title, content } = req.body;
    
    const newNews = new News({ title, content });
    
    newNews.save()
        .then(news => res.status(201).json(news))
        .catch(err => res.status(400).json({ error: err.message }));
});

app.get('/news', (req, res) => {
    News.find()
        .then(news => res.json(news))
        .catch(err => res.status(400).json({ error: err.message }));
});

app.post('/contact', (req, res) => {
    const { name, email, message } = req.body;
    
    const newContact = new Contact({ name, email, message });
    
    newContact.save()
        .then(contact => res.status(201).json(contact))
        .catch(err => res.status(400).json({ error: err.message }));
});

app.post('/collaborate', (req, res) => {
    const { name, email, proposal } = req.body;
    
    const newCollaboration = new Collaboration({ name, email, proposal });
    
    newCollaboration.save()
        .then(collaboration => res.status(201).json(collaboration))
        .catch(err => res.status(400).json({ error: err.message }));
});

app.listen(PORT, () => {
    console.log(`Server running on http://localhost:${PORT}`);
});
