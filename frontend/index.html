// ─────────────────────────────────────────────────────────────
//  Ritam AI — Backend Server
//  Provides API endpoints for ScentAI and DriveIQ frontends
//  Uses OpenAI API for intelligent recommendations
// ─────────────────────────────────────────────────────────────

require('dotenv').config();
const express = require('express');
const cors = require('cors');
const { OpenAI } = require('openai');

const app = express();
const PORT = process.env.PORT || 3000;

// ── Middleware ──
app.use(cors({
    origin: process.env.ALLOWED_ORIGINS
        ? process.env.ALLOWED_ORIGINS.split(',')
        : ['http://localhost:5500', 'http://127.0.0.1:5500', 'http://localhost:3000'],
    methods: ['GET', 'POST'],
    credentials: true
}));
app.use(express.json({ limit: '1mb' }));

// ── OpenAI Client ──
const openai = new OpenAI({
    apiKey: process.env.OPENAI_API_KEY
});

// ── Health Check ──
app.get('/api/health', (req, res) => {
    res.json({
        status: 'ok',
        timestamp: new Date().toISOString(),
        services: {
            fragrance: 'active',
            car: 'active'
        }
    });
});


// ═══════════════════════════════════════════════════════════════
//  FRAGRANCE AI ENDPOINT
// ═══════════════════════════════════════════════════════════════

const FRAGRANCE_SYSTEM_PROMPT = `You are ScentAI, an expert fragrance advisor with deep knowledge of perfumery. You have extensive knowledge of fragrances from all major houses (Dior, Chanel, Tom Ford, Creed, Maison Francis Kurkdjian, Parfums de Marly, Nishane, Xerjoff, etc.) as well as affordable options (Zara, Lattafa, Armaf, Al Rehab, etc.).

Your expertise includes:
- Fragrance families and note pyramids (top, heart, base notes)
- Longevity and projection characteristics
- Seasonal and occasion appropriateness
- Clone/dupe recommendations for expensive fragrances
- Layering combinations
- Price-to-value analysis
- Current trending fragrances and new releases

Guidelines for responses:
1. Always provide SPECIFIC fragrance names with the house/brand
2. Include key notes when recommending a fragrance
3. Mention approximate price ranges when relevant
4. Suggest 3-5 options at different price points when asked for recommendations
5. If the user mentions a fragrance they like, suggest similar options AND complementary alternatives
6. Use formatting: **bold** for fragrance names, bullet points for lists
7. Be conversational and passionate about fragrances — you love this stuff
8. When you know a great affordable clone/dupe, mention it
9. Consider the user's stated preferences (occasion, season, budget, notes) in every response
10. Reference real fragrance data — note pyramids, longevity reports, community ratings`;

app.post('/api/fragrance', async (req, res) => {
    try {
        const { message, preferences, history = [] } = req.body;

        if (!message) {
            return res.status(400).json({ error: 'Message is required' });
        }

        // Build context from preferences
        let prefContext = '';
        if (preferences) {
            const parts = [];
            if (preferences.occasion) parts.push(`Occasion: ${preferences.occasion}`);
            if (preferences.season) parts.push(`Season: ${preferences.season}`);
            if (preferences.gender) parts.push(`Gender preference: ${preferences.gender}`);
            if (preferences.budget) parts.push(`Budget: ${preferences.budget}`);
            if (preferences.preferredNotes?.length > 0) {
                parts.push(`Preferred notes: ${preferences.preferredNotes.join(', ')}`);
            }
            if (parts.length > 0) {
                prefContext = `\n\n[User preferences: ${parts.join(' | ')}]`;
            }
        }

        // Build message history for context
        const messages = [
            { role: 'system', content: FRAGRANCE_SYSTEM_PROMPT + prefContext }
        ];

        // Add conversation history (last 10 messages)
        for (const msg of history.slice(-10)) {
            messages.push({
                role: msg.role,
                content: msg.content
            });
        }

        // Add current message if not already in history
        if (!history.length || history[history.length - 1]?.content !== message) {
            messages.push({ role: 'user', content: message });
        }

        const completion = await openai.chat.completions.create({
            model: process.env.OPENAI_MODEL || 'gpt-4o-mini',
            messages,
            temperature: 0.8,
            max_tokens: 1000
        });

        const reply = completion.choices[0]?.message?.content || 'I couldn\'t generate a response. Please try again.';

        res.json({ reply });

    } catch (error) {
        console.error('[Fragrance API Error]', error.message);

        if (error.status === 401) {
            return res.status(500).json({
                error: 'Invalid API key. Check your OPENAI_API_KEY in .env'
            });
        }
        if (error.status === 429) {
            return res.status(429).json({
                error: 'Rate limit exceeded. Please wait a moment and try again.'
            });
        }

        res.status(500).json({
            error: 'Something went wrong with the fragrance advisor.',
            details: process.env.NODE_ENV === 'development' ? error.message : undefined
        });
    }
});


// ═══════════════════════════════════════════════════════════════
//  CAR DEAL AI ENDPOINT
// ═══════════════════════════════════════════════════════════════

const CAR_SYSTEM_PROMPT = `You are DriveIQ, an expert car deal analyst and negotiation coach. You combine the knowledge of a seasoned car buyer, a dealership finance manager, and a consumer advocate.

Your expertise includes:
- Fair market values for new and used vehicles (based on KBB, Edmunds, NADA ranges)
- Depreciation curves and when cars hit their value sweet spots
- Common dealership tactics and how to counter them
- Detailed negotiation scripts buyers can use word-for-word
- Hidden fees and add-ons to watch for (dealer prep, VIN etching, paint protection, extended warranties)
- Reliability ratings and known issues by make/model/year
- Total cost of ownership (insurance, maintenance, fuel)
- When to walk away from a deal
- Trade-in value optimization

Guidelines for responses:
1. When analyzing a specific car deal, always provide:
   - A deal verdict: **Great Deal**, **Good Deal**, **Fair Deal**, **Below Average**, or **Bad Deal**
   - Estimated fair market value range
   - Specific reasons why it's good or bad
   - 3-5 negotiation tactics specific to that vehicle
2. Use formatting: **bold** for key terms, bullet points for lists, ### for section headers
3. Be direct and confident — users are counting on your honesty
4. When suggesting negotiation tactics, provide actual phrases/scripts they can say
5. Always mention potential red flags (rebuilt title, flood damage, high mileage for year, etc.)
6. Consider the user's priorities (reliability, fuel economy, performance, etc.)
7. If a deal seems too good to be true, say so and explain why
8. Reference real-world data points — reliability rankings, depreciation rates, common issues
9. Tone: Professional but approachable. Think trusted friend who happens to be a car expert.
10. Never sugarcoat a bad deal — the user needs to know the truth`;

app.post('/api/car', async (req, res) => {
    try {
        const { message, carDetails, history = [] } = req.body;

        if (!message) {
            return res.status(400).json({ error: 'Message is required' });
        }

        // Build context from car details
        let carContext = '';
        if (carDetails) {
            const parts = [];
            if (carDetails.make) parts.push(`Make: ${carDetails.make}`);
            if (carDetails.model) parts.push(`Model: ${carDetails.model}`);
            if (carDetails.year) parts.push(`Year: ${carDetails.year}`);
            if (carDetails.mileage) parts.push(`Mileage: ${Number(carDetails.mileage).toLocaleString()}`);
            if (carDetails.price) parts.push(`Asking price: $${Number(carDetails.price).toLocaleString()}`);
            if (carDetails.condition) parts.push(`Condition: ${carDetails.condition}`);
            if (carDetails.priorities?.length > 0) {
                parts.push(`Buyer priorities: ${carDetails.priorities.join(', ')}`);
            }
            if (parts.length > 0) {
                carContext = `\n\n[Vehicle details provided: ${parts.join(' | ')}]`;
            }
        }

        // Build message history
        const messages = [
            { role: 'system', content: CAR_SYSTEM_PROMPT + carContext }
        ];

        for (const msg of history.slice(-10)) {
            messages.push({
                role: msg.role,
                content: msg.content
            });
        }

        if (!history.length || history[history.length - 1]?.content !== message) {
            messages.push({ role: 'user', content: message });
        }

        const completion = await openai.chat.completions.create({
            model: process.env.OPENAI_MODEL || 'gpt-4o-mini',
            messages,
            temperature: 0.7,
            max_tokens: 1200
        });

        const reply = completion.choices[0]?.message?.content || 'I couldn\'t generate a response. Please try again.';

        res.json({ reply });

    } catch (error) {
        console.error('[Car API Error]', error.message);

        if (error.status === 401) {
            return res.status(500).json({
                error: 'Invalid API key. Check your OPENAI_API_KEY in .env'
            });
        }
        if (error.status === 429) {
            return res.status(429).json({
                error: 'Rate limit exceeded. Please wait a moment and try again.'
            });
        }

        res.status(500).json({
            error: 'Something went wrong with the car advisor.',
            details: process.env.NODE_ENV === 'development' ? error.message : undefined
        });
    }
});


// ═══════════════════════════════════════════════════════════════
//  START SERVER
// ═══════════════════════════════════════════════════════════════

app.listen(PORT, () => {
    console.log(`
╔══════════════════════════════════════════════════╗
║            Ritam AI — Backend Server             ║
╠══════════════════════════════════════════════════╣
║  Status:    Running                              ║
║  Port:      ${String(PORT).padEnd(37)}║
║  Endpoints:                                      ║
║    POST /api/fragrance  →  ScentAI advisor       ║
║    POST /api/car        →  DriveIQ advisor       ║
║    GET  /api/health     →  Status check          ║
╚══════════════════════════════════════════════════╝
    `);

    if (!process.env.OPENAI_API_KEY) {
        console.warn('⚠️  WARNING: OPENAI_API_KEY is not set in .env file.');
        console.warn('   The AI endpoints will fail without a valid API key.');
        console.warn('   Copy .env.example to .env and add your key.\n');
    }
});
