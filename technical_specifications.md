# Home Apothecary Website - Technical Specification Summary

## Quick Reference Guide

---

## 1. RECOMMENDED TECHNOLOGY STACK

### Platform: **WordPress**
**Why:** Easy to manage, proven for membership sites, no coding required

### Essential Plugins/Services:

| Purpose | Tool | Cost |
|---------|------|------|
| Membership Management | MemberPress | $249/year |
| Payment Processing | Stripe | 2.9% + $0.30/transaction |
| Video Hosting | Vimeo Plus | $144/year |
| Email Marketing | Mailchimp (start) | Free up to 500 subscribers |
| SEO | Yoast SEO | Free |
| Forms | WPForms Lite | Free |
| Comments | Disqus or native WP | Free |
| Security | Wordfence | Free |
| Backups | UpdraftPlus | Free |
| Speed | WP Rocket | $59/year (optional) |

**Total Year 1 Tech Cost: ~$650-900**

---

## 2. WEBSITE STRUCTURE MAP

```
┌─────────────────────────────────────────────────────────────┐
│                         HOME PAGE                            │
│  - Hero: "Natural Remedies You Can Make at Home"           │
│  - Featured Categories                                       │
│  - Latest Recipes                                            │
│  - Video Testimonials                                        │
│  - Subscribe CTA                                             │
└─────────────────────────────────────────────────────────────┘
                              │
        ┌─────────────────────┼─────────────────────┐
        │                     │                     │
        ▼                     ▼                     ▼
┌──────────────┐    ┌──────────────┐    ┌──────────────┐
│  CATEGORIES  │    │  MEMBERSHIP  │    │  COMMUNITY   │
│              │    │              │    │              │
│ • Cardiovas  │    │ • Plans      │    │ • Discussions│
│ • Respiratory│    │ • Sign Up    │    │ • Success    │
│ • Digestive  │    │ • Login      │    │ • Q&A        │
│ • (Future)   │    │ • Account    │    │              │
└──────────────┘    └──────────────┘    └──────────────┘
        │
        │
        ▼
┌─────────────────────────────────────────┐
│     CATEGORY: Cardiovascular System     │
│                                         │
│  Ailments (Sub-categories):             │
│  ├── Blood Pressure                    │
│  ├── Cholesterol Management            │
│  ├── Circulatory Health                │
│  ├── Heart Health                      │
│  └── Arterial Health                   │
└─────────────────────────────────────────┘
                    │
                    ▼
┌──────────────────────────────────────────────────────┐
│            RECIPE DETAIL PAGE                        │
│                                                      │
│  ┌────────────────────────────────────────────────┐ │
│  │ Recipe Title: "Cinnamon Infusion"              │ │
│  │ Ailment: Blood Pressure                        │ │
│  └────────────────────────────────────────────────┘ │
│                                                      │
│  [Hero Image/Video Thumbnail]                       │
│                                                      │
│  ┌─ Quick Info ──────────────────────────────────┐  │
│  │ 👤 Adults: Yes  👶 Children: Caution          │  │
│  │ 📊 Prep Ease: 5/5  🛒 Sourcing: 5/5          │  │
│  └───────────────────────────────────────────────┘  │
│                                                      │
│  📝 Description                                      │
│  [Educational overview paragraph]                    │
│                                                      │
│  🔬 Detailed Benefits                                │
│  [Sub-description paragraph]                         │
│                                                      │
│  🥄 Ingredients                                      │
│  • Ingredient 1                                      │
│  • Ingredient 2                                      │
│                                                      │
│  🎥 VIDEO TUTORIAL                                   │
│  [Embedded Video Player]                             │
│                                                      │
│  📋 Step-by-Step Instructions                        │
│  1. First step...                                    │
│  2. Second step...                                   │
│                                                      │
│  💊 Dosage & Usage                                   │
│  [Dosage information]                                │
│                                                      │
│  ⚠️ Important Notes & Cautions                       │
│  [Safety warnings highlighted]                       │
│                                                      │
│  ❤️ Save Recipe  🖨️ Print Recipe                    │
│                                                      │
│  💬 COMMENTS & COMMUNITY DISCUSSION                  │
│  [Comment thread with replies]                       │
│                                                      │
│  🔗 Related Recipes                                  │
│  [3-4 similar recipe cards]                          │
└──────────────────────────────────────────────────────┘
```

---

## 3. DATABASE SCHEMA (Simplified)

### WordPress Custom Post Types:

**Post Type: `recipe`**
- Recipe title
- Recipe slug (URL-friendly)
- Featured image
- Video URL
- Recipe content (description)

**Taxonomies:**
- `category` (Cardiovascular, Respiratory, etc.)
- `ailment` (Blood Pressure, Cholesterol, etc.)

**Custom Fields (using ACF or Pods):**
```
recipe_sub_description (text area)
ingredients (WYSIWYG or repeater)
preparation_notes (text area)
instructions (WYSIWYG or repeater)
dosage (text)
cautions (text area)
ease_of_prep (number 1-5)
ease_of_sourcing (number 1-5)
suitable_adults (true/false)
suitable_children (true/false)
video_url (URL)
video_thumbnail (image)
prep_time (text)
```

### MemberPress Membership Levels:
1. Free (sample access)
2. Monthly ($9.99)
3. Annual ($99)
4. Premium ($19.99)

---

## 4. USER FLOW DIAGRAM

### New Visitor Journey:
```
Homepage
    │
    ├─→ Browse Recipes (limited preview) ─→ Hit paywall
    │                                           │
    │                                           ▼
    │                                    Sign Up Page
    │                                           │
    │                                           ├─→ Free Tier
    │                                           └─→ Paid Tier
    │                                                   │
    └───────────────────────────────────────────────────┘
                                                        │
                                                        ▼
                                            Member Dashboard
                                                        │
                                        ┌───────────────┼───────────────┐
                                        ▼               ▼               ▼
                                  Browse All      Saved Recipes   Community
                                   Recipes
                                        │
                                        ▼
                                Recipe Detail Page
                                        │
                        ┌───────────────┼───────────────┐
                        ▼               ▼               ▼
                   Watch Video    Post Comment    Save Recipe
```

### Member Experience:
```
Login ─→ Dashboard
          │
          ├─→ Browse by Category ─→ View Recipe ─→ Watch Video
          │                                     └─→ Comment
          │                                     └─→ Save/Print
          │
          ├─→ My Saved Recipes ─→ Access quickly
          │
          ├─→ Community Hub ─→ Participate in discussions
          │
          └─→ Account Settings ─→ Manage subscription
```

---

## 5. VIDEO PRODUCTION SPECIFICATIONS

### Technical Specs:
- **Resolution:** 1080p (1920x1080)
- **Aspect Ratio:** 16:9
- **Frame Rate:** 24fps or 30fps
- **Format:** MP4 (H.264 codec)
- **Audio:** 48kHz, stereo
- **Length:** 5-10 minutes per recipe

### Filming Setup:
```
┌──────────────────────────────────────┐
│         Overhead Camera View          │
│                                       │
│    [Ingredients]  [Work Surface]     │
│                                       │
│         ↓ Tripod/Mount               │
│        📱 Camera                      │
│                                       │
│    💡 Light    Person    💡 Light    │
│                                       │
│         🎤 Microphone                 │
└──────────────────────────────────────┘
```

### Video Structure Template:
1. **Intro (15 sec)**
   - Recipe name overlay
   - Quick benefit statement
   - Welcoming message

2. **Ingredients Display (30 sec)**
   - Show all ingredients laid out
   - Name each item clearly

3. **Preparation Steps (4-7 min)**
   - Clear, step-by-step demonstration
   - Close-ups of key techniques
   - Real-time or slightly sped up

4. **Final Product (30 sec)**
   - Show finished remedy
   - How to store

5. **Usage & Dosage (1 min)**
   - How to consume/apply
   - Frequency recommendations

6. **Safety Reminder (30 sec)**
   - Key cautions highlighted
   - "Consult healthcare provider" message

7. **Outro (15 sec)**
   - Subscribe/comment call-to-action
   - Related recipes teaser

---

## 6. MEMBERSHIP SUBSCRIPTION LOGIC

### Subscription Tiers & Access Matrix:

| Feature | Free | Monthly | Annual | Premium |
|---------|------|---------|--------|---------|
| Sample recipes (5) | ✅ | ✅ | ✅ | ✅ |
| All recipes | ❌ | ✅ | ✅ | ✅ |
| Video tutorials | Limited | ✅ | ✅ | ✅ |
| Community comments | Read-only | ✅ | ✅ | ✅ |
| Save recipes | ❌ | ✅ | ✅ | ✅ |
| Printable PDFs | ❌ | ✅ | ✅ | ✅ |
| Monthly newsletter | ✅ | ✅ | ✅ | ✅ |
| Early access | ❌ | ❌ | ✅ | ✅ |
| Live webinars | ❌ | ❌ | ❌ | ✅ |
| Direct messaging | ❌ | ❌ | ❌ | ✅ |
| Personal recommendations | ❌ | ❌ | ❌ | ✅ |

### Payment Flow:
```
User clicks "Subscribe"
    │
    ▼
Select plan page
    │
    ├─→ Monthly ($9.99/month)
    ├─→ Annual ($99/year) [BEST VALUE badge]
    └─→ Premium ($19.99/month)
    │
    ▼
Checkout page (Stripe)
    │
    ├─→ Email
    ├─→ Payment details
    └─→ Create account
    │
    ▼
Payment processing (Stripe)
    │
    ├─→ Success ─→ Welcome email ─→ Access granted
    │
    └─→ Failure ─→ Error message ─→ Try again
```

---

## 7. CONTENT UPLOAD WORKFLOW

### Adding a New Recipe (Admin Workflow):

```
1. Create New Post
   └─→ Select post type: "Recipe"

2. Fill in Basic Info
   ├─→ Recipe title
   ├─→ Upload featured image
   └─→ Select categories (Health System + Ailment)

3. Add Recipe Content
   ├─→ Description (main editor)
   ├─→ Sub-description (custom field)
   ├─→ Ingredients (custom field/repeater)
   ├─→ Instructions (custom field/repeater)
   ├─→ Preparation notes (custom field)
   ├─→ Dosage (custom field)
   └─→ Cautions (custom field)

4. Add Video
   ├─→ Upload to Vimeo
   ├─→ Copy embed URL
   ├─→ Paste into video URL field
   └─→ Add video thumbnail

5. Set Metadata
   ├─→ Ease of prep (1-5)
   ├─→ Ease of sourcing (1-5)
   ├─→ Suitable for adults (yes/no)
   ├─→ Suitable for children (yes/caution/no)
   └─→ Prep time

6. Access Control
   └─→ Set to "Members Only" or specific tier

7. SEO Optimization
   ├─→ Write meta description
   ├─→ Add focus keyword
   └─→ Add alt text to images

8. Preview & Test
   └─→ Check mobile responsiveness

9. Publish
   └─→ Schedule or publish immediately

10. Announce
    ├─→ Send email to subscribers
    ├─→ Post on social media
    └─→ Update homepage featured recipes
```

---

## 8. SAFETY & LEGAL IMPLEMENTATION

### Required Website Elements:

**1. Global Medical Disclaimer (appears on every page, footer):**
```html
<div class="medical-disclaimer">
  ⚕️ Medical Disclaimer: This information is for educational 
  purposes only and not intended as medical advice. Consult a 
  healthcare provider before starting any new health regimen.
</div>
```

**2. Recipe-Specific Warning Box (prominent on each recipe):**
```html
<div class="caution-box">
  ⚠️ IMPORTANT SAFETY INFORMATION
  [Specific cautions for this recipe]
  
  - Medication interactions
  - Allergies
  - Age restrictions
  - When to consult doctor
</div>
```

**3. User Agreement Checkbox (at registration):**
```
☐ I understand these are educational remedies and not medical 
  advice. I will consult my healthcare provider before trying 
  new remedies, especially if I have medical conditions or 
  take medications.
```

**4. Legal Pages (linked in footer):**
- Terms of Service
- Privacy Policy (GDPR/CCPA compliant)
- Cookie Policy
- Refund Policy
- Medical Disclaimer (full page)
- Contact/Support

---

## 9. ANALYTICS & TRACKING SETUP

### Essential Metrics to Track:

**Google Analytics Events:**
```javascript
// Track video plays
gtag('event', 'video_play', {
  'recipe_name': 'Cinnamon Infusion',
  'category': 'Cardiovascular'
});

// Track recipe saves
gtag('event', 'recipe_save', {
  'recipe_name': 'Cinnamon Infusion'
});

// Track subscription starts
gtag('event', 'subscription_start', {
  'plan': 'Monthly',
  'value': 9.99
});

// Track comments posted
gtag('event', 'comment_post', {
  'recipe_name': 'Cinnamon Infusion'
});
```

### Dashboard Metrics:
- Daily active users
- New subscriptions (by tier)
- Churn rate
- Most viewed recipes
- Video completion rate
- Average session duration
- Search queries
- Failed payment attempts
- Comment activity

---

## 10. MOBILE RESPONSIVENESS REQUIREMENTS

### Mobile-First Checklist:

✅ **Navigation:**
- Hamburger menu on mobile
- Touch-friendly buttons (min 44x44px)
- Easy access to search

✅ **Recipe Pages:**
- Readable text (min 16px font)
- Tappable ingredient checkboxes
- Video player adapts to screen
- Print button accessible
- Comments easy to read/write

✅ **Video Player:**
- Responsive iframe embed
- Full-screen option
- Playback controls accessible
- Load speed optimized

✅ **Forms:**
- Large input fields
- Auto-zoom disabled on inputs
- Payment form mobile-optimized
- Error messages clear

✅ **Images:**
- Lazy loading
- Compressed for mobile
- Retina-ready (@2x)

### Testing Devices:
- iPhone (Safari)
- Android (Chrome)
- iPad (Safari)
- Desktop (Chrome, Firefox, Safari, Edge)

---

## 11. LAUNCH CHECKLIST

### Pre-Launch (1 week before):

- [ ] All plugins tested and working
- [ ] Payment processing tested (Stripe test mode)
- [ ] At least 10 recipes published with videos
- [ ] All legal pages completed
- [ ] Email sequences set up
- [ ] Analytics installed and tracking
- [ ] Mobile responsiveness verified
- [ ] SSL certificate active (HTTPS)
- [ ] Backup system configured
- [ ] Security plugins active
- [ ] Contact forms working
- [ ] Social media profiles created
- [ ] Terms of service agreed at checkout
- [ ] Welcome email template created
- [ ] 404 error page customized

### Launch Day:

- [ ] Switch Stripe to live mode
- [ ] Send launch email to list
- [ ] Post on all social channels
- [ ] Update Google My Business
- [ ] Submit sitemap to Google
- [ ] Monitor for errors/issues
- [ ] Be available for support questions

### Post-Launch (Week 1):

- [ ] Monitor analytics daily
- [ ] Respond to all comments/questions
- [ ] Fix any bugs reported
- [ ] Collect user feedback
- [ ] Send thank you email to first subscribers
- [ ] Post success metrics on social
- [ ] Schedule next batch of content

---

## 12. COST SUMMARY

### One-Time Costs:
| Item | Cost |
|------|------|
| Domain name | $15 |
| Premium theme | $60 |
| Logo design (optional) | $200-500 |
| Stock photos | $100 |
| Video equipment | $200-1000 |
| **Total One-Time:** | **$575-1,675** |

### Annual Costs:
| Item | Cost |
|------|------|
| Hosting | $120-300 |
| MemberPress | $249 |
| Vimeo Plus | $144 |
| Email marketing | $0-300 |
| Domain renewal | $15 |
| **Total Annual:** | **$528-1,008** |

### Monthly Costs:
| Item | Cost |
|------|------|
| Average monthly | $44-84 |

### Revenue Projections (Month 6):
- 150 subscribers @ $9.99/mo = $1,498/mo
- Minus Stripe fees (3%) = **$1,453/mo**
- Minus costs ($84/mo) = **$1,369/mo profit**

### Break-even Point:
- Need ~10-15 paying subscribers to cover costs
- Achievable within first 1-2 months

---

## QUICK START SUMMARY

**Week 1-2:** Set up WordPress, install plugins, choose theme
**Week 3-4:** Design site, create templates, upload content
**Week 5-6:** Film and upload videos, test everything
**Week 7-8:** Beta launch, collect feedback, official launch

**Budget:** $1,000-2,000 to start
**Time to Launch:** 6-8 weeks
**Break-even:** 10-15 subscribers

**Next Immediate Steps:**
1. Buy domain name
2. Sign up for hosting
3. Install WordPress
4. Install MemberPress
5. Film first 5 videos

---

*This technical specification provides the foundation to build your Home Apothecary website. Refer to the full project plan for detailed strategic guidance.*
