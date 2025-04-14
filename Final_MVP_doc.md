# AI-Driven Personalized Onboarding: Hackathon MVP
**Author**: [Your Name]  
**Date**: April 14, 2025

## 1. Hackathon Solution Overview

### 1.1. Elevator Pitch

We're building an AI-powered personalization layer for Razorpay's onboarding that automatically identifies high-value merchants through external data enrichment and provides them with an elevated, agent-assisted onboarding experience. Our hackathon MVP demonstrates an end-to-end happy flow for high-value merchants, from signup to first transaction.

### 1.2. Problem Statement

Despite improvements from Modular Onboarding, we face critical issues:
- One-size-fits-all experience regardless of merchant value
- Only 8.72% signup-to-MTU conversion overall
- High-value merchants (0.3% of users generating 90% of GMV) face the same friction as all others
- Current HQL detection has low accuracy (39% precision, 15% recall)
- High-value merchants experience more support issues (13 SVs per merchant vs. 2.1 average)

### 1.3. Hackathon Solution Scope

For this 24-hour hackathon, we'll focus on building:

1. **Automated HQL Identification System**:
   - Business data enrichment from email domain
   - External data integration (website traffic, GSTIN, LinkedIn, Crunchbase)
   - Intelligent scoring and HQL classification

2. **AI-Agent Assisted Experience for HQLs**:
   - Video call-like interface with AI agent
   - Proactive document assistance and explanation
   - Simplified document verification through pre-filled information

3. **Post-Activation Guidance**:
   - Personalized dashboard onboarding
   - First transaction walkthrough
   - Custom pricing suggestions

## 2. Technical Approach

### 2.1. Key Components

1. **Data Enrichment Pipeline**:
   - Email domain analysis for business identification
   - Website scraping for business information
   - GSTIN lookup and data extraction
   - Company profiling via LinkedIn/Crunchbase APIs

2. **HQL Classification System**:
   - Multi-factor scoring algorithm
   - Threshold-based classification
   - Business type, traffic, turnover and funding analysis

3. **AI-Agent Interface**:
   - Video call-like UI with animated agent
   - Natural language understanding for merchant questions
   - Context-aware responses and guidance

4. **Simplified Documentation Process**:
   - Auto-fetching of business documents (CoI, CIN)
   - Pre-filling information from GSTIN/PAN
   - QR-based UPI verification alternative to bank details

5. **Post-Activation Experience**:
   - Interactive dashboard tutorial
   - Guided first transaction flow
   - Dynamic pricing recommendation engine

### 2.2. End-to-End Happy Flow

For our demo, we'll implement this end-to-end flow for high-value merchants:

1. **Initial Signup**:
   - User enters work email (e.g., name@enterprise.com)
   - System extracts domain and identifies company
   - Background enrichment process starts

2. **Data Enrichment**:
   - System fetches business name, website, business type
   - Retrieves website traffic stats
   - Looks up GSTIN and extracts turnover information
   - Gets employee count and funding data (for funded startups)
   - Classifies as HQL based on criteria (Private Limited + high traffic + high turnover)

3. **Enhanced HQL Experience**:
   - AI agent appears in video call-like interface
   - Welcomes merchant by name and company
   - Explains streamlined process for high-value businesses

4. **Simplified KYC Collection**:
   - Agent asks for business PAN number
   - System auto-fetches CIN, CoI document, business address
   - Agent explains that authorised signatories have been identified
   - Requests bank account details (number + IFSC) or offers QR payment option
   - Asks for Aadhaar card upload for one of the pre-identified signatories

5. **Verification Process**:
   - Shows real-time verification status
   - For successful verification: activates account immediately
   - For failed verification: communicates 24-hour manual review process

6. **Post-Activation Guidance**:
   - Smooth transition to dashboard 
   - Interactive tutorial highlighting key features
   - Step-by-step guide to completing first transaction
   - Presents custom pricing options based on projected GMV

## 3. Implementation Plan (24 Hours)

### Hour 1-4: Setup and Planning
- Configure development environment in Lovable
- Set up mock APIs for data enrichment services
- Design AI agent interface and interaction patterns

### Hour 5-10: Data Enrichment & HQL Classification
- Build email domain analyzer and mock data responses
- Create HQL scoring algorithm based on business criteria
- Implement threshold-based classification system
- Design status indicators and loading states

### Hour 11-16: AI Agent & KYC Flow
- Develop video call-like interface with animated agent
- Create conversation flow for KYC collection
- Build auto-population of fields from "fetched" data
- Implement document upload component with verification status

### Hour 17-22: Post-Activation & Integration
- Build dashboard tutorial experience
- Create first transaction guided walkthrough
- Implement custom pricing recommendation display
- Connect all components into end-to-end flow

### Hour 23-24: Finalization and Preparation
- Polish UI and animations
- Create demo script showing full happy path
- Prepare alternative paths for presentation
- Document approach and potential impact

## 4. Demo Scenario: Enterprise HQL Flow

Our demo will showcase the following journey for a high-value enterprise merchant:

### Scenario: High-Value Enterprise Lead
- User signs up with corporate email (e.g., finance@enterprise-corp.com)
- System identifies as a Private Limited company with ₹10Cr+ turnover
- System detects 100K+ monthly visitors to their website
- AI agent appears, greeting by company name and position
- Agent explains the streamlined verification process
- User enters business PAN, system auto-fills company details
- User confirms bank account via UPI QR scan
- User uploads required Aadhaar document
- Verification completes successfully
- Agent guides user to dashboard and through first transaction setup
- System presents custom pricing proposal based on projected volume

## 5. Expected Impact

If implemented in production, our solution would drive:

1. **Conversion Improvements**:
   - Increase HQL conversion rate by 60% (from current baseline)
   - Reduce KYC completion time for high-value merchants by 70%

2. **Operational Efficiency**:
   - Decrease manual verification requirements by 50% for HQL segments
   - Reduce support ticket volume from high-value merchants by 65%

3. **Business Impact**:
   - Faster time to first transaction for high-GMV merchants (3 hours vs current 3 days)
   - Improved retention of top-tier merchants (90%+ vs current 86%)
   - Higher average GMV per merchant through better targeting

## 6. Technical Requirements for Hack Day

For the hackathon prototype, we'll need:

1. **Frontend Components**:
   - Video call-like interface with animated AI agent
   - Dynamic form fields with auto-population
   - Progress indicators and verification status displays
   - Dashboard tutorial overlay system

2. **Mock Backend Services**:
   - API response mocks for business data enrichment
   - HQL classification logic
   - Document verification simulation
   - Custom pricing recommendation engine

3. **Data Visualization**:
   - Visual representation of HQL scoring
   - Real-time verification status indicators
   - Custom pricing proposal charts

## 7. Implementation Details

### 7.1. HQL Classification Logic

```javascript
// HQL Classification Algorithm
function classifyMerchant(merchantData) {
  // Initialize score
  let isHQL = false;
  
  // Check primary criteria
  const isPrivateLimited = merchantData.businessType === "Private Limited" || 
                           merchantData.businessType === "Public Limited";
  
  const hasHighTraffic = merchantData.websiteTraffic > 50000; // Monthly visitors
  
  const hasHighTurnover = merchantData.gstinTurnover > 50000000; // 5 Crore+
  
  // Additional signals
  const hasSignificantEmployees = merchantData.employeeCount > 50;
  
  const hasFunding = merchantData.fundingRounds && merchantData.fundingRounds.length > 0;
  
  // Primary classification
  if (isPrivateLimited && (hasHighTraffic || hasHighTurnover)) {
    isHQL = true;
  }
  
  // Secondary classification
  if (!isHQL && isPrivateLimited && (hasSignificantEmployees || hasFunding)) {
    isHQL = true;
  }
  
  // Assign experience tier
  let experienceTier = "STANDARD";
  
  if (isHQL) {
    experienceTier = hasHighTurnover && hasHighTraffic ? "PRIORITY" : "ENHANCED";
  }
  
  return {
    isHQL,
    experienceTier,
    reasoning: {
      isPrivateLimited,
      hasHighTraffic,
      hasHighTurnover,
      hasSignificantEmployees,
      hasFunding
    }
  };
}
```

### 7.2. Data Enrichment Flow

```javascript
// Data Enrichment Pipeline
async function enrichMerchantData(email) {
  try {
    // Extract domain from email
    const domain = email.split('@')[1];
    
    // Fetch company information from domain
    const companyInfo = await fetchCompanyFromDomain(domain);
    
    // Parallel data enrichment
    const [
      websiteData,
      gstinData,
      companyProfileData
    ] = await Promise.all([
      fetchWebsiteTrafficData(companyInfo.website),
      fetchGSTINData(companyInfo.name),
      fetchCompanyProfileData(companyInfo.name)
    ]);
    
    // Combine all data
    const enrichedData = {
      email,
      domain,
      businessName: companyInfo.name,
      businessType: companyInfo.type || companyProfileData.businessType,
      website: companyInfo.website,
      websiteTraffic: websiteData.monthlyVisitors,
      gstinNumber: gstinData.number,
      gstinTurnover: gstinData.annualTurnover,
      employeeCount: companyProfileData.employeeCount,
      fundingRounds: companyProfileData.fundingRounds,
      authorizedSignatories: gstinData.directors || []
    };
    
    // Classify merchant
    const classification = classifyMerchant(enrichedData);
    
    return {
      ...enrichedData,
      ...classification
    };
  } catch (error) {
    console.error("Error enriching merchant data:", error);
    return {
      email,
      isHQL: false,
      experienceTier: "STANDARD",
      error: true
    };
  }
}
```

### 7.3. AI Agent Conversation Flow

The AI agent will follow this conversation flow for HQLs:

1. **Welcome & Introduction**:
   ```
   "Welcome to Razorpay, [Name]! I'm Maya, your dedicated onboarding specialist. I see you're from [Company Name], a leading [Industry] company. I'll be guiding you through our streamlined verification process for business partners like yours."
   ```

2. **Process Overview**:
   ```
   "We've already gathered some information about [Company Name] to make this process as smooth as possible. I'll just need to confirm a few details with you, and we can have your account activated quickly so you can start accepting payments."
   ```

3. **PAN Collection**:
   ```
   "Could you please share your business PAN number? This will help us verify your company information and auto-fill several fields for you."
   ```

4. **Information Confirmation**:
   ```
   "Great! I've found your company details. I can confirm [Company Name] is registered as a [Business Type] with registered address at [Address]. Is this information correct?"
   ```

5. **Bank Details**:
   ```
   "Now, I'll need to verify your business bank account. You can either provide your account number and IFSC code, or simply scan this QR code with your UPI app to make a ₹1 verification payment that will be refunded immediately."
   ```

6. **Document Request**:
   ```
   "Finally, I need to verify one of your authorized signatories. Our records show [Signatory Names]. Please upload the Aadhaar card for any one of these individuals."
   ```

7. **Verification Status**:
   ```
   "Perfect! We're processing your verification now. This typically takes just a few moments for accounts like yours."
   ```

8. **Success & Next Steps**:
   ```
   "Congratulations! Your account is now activated. Let me guide you through your dashboard and help you set up your first transaction. I'll also show you some custom pricing options we've prepared based on your expected transaction volume."
   ```

### 7.4. UI Components for HQL Experience

#### 1. AI Agent Video Interface
- Full-screen modal overlay with semi-transparent background
- Video-call style interface with animated AI agent
- Typing indicator when agent is "thinking"
- Subtle facial expressions and gestures during interaction
- Option to minimize or expand the agent window

#### 2. Smart KYC Form
- Clean, minimal form design with large input fields
- Real-time validation with instant feedback
- "Auto-filling" animation when pulling data from external sources
- Visual progress through verification steps
- Document upload area with preview and verification status

#### 3. Verification Status Display
- Circular progress indicator for overall verification
- Individual status indicators for each verification step
- Success animations for completed verifications
- Estimated time remaining for processing

#### 4. Dashboard Tutorial Overlay
- Spotlight highlights for key dashboard elements
- Step-by-step guidance panels
- Interactive clickable elements
- Progress tracker for onboarding completion
- "Skip for now" option with ability to resume later

#### 5. Custom Pricing Display
- Visual comparison of standard vs. custom pricing
- Projected savings calculator
- Volume-based tier explanation
- One-click acceptance option