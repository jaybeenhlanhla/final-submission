/**
 * GUTS & GUYS - Form Validation & Processing (js/validation.js)
 * Covers Enquiry Price Calculation & Contact Email Assembly
 */

document.addEventListener('DOMContentLoaded', () => {
    initEnquiryForm();
    initContactForm();
});

/* ==========================================================================
   4.1. Enquiry Form Logic & Cost Calculation Processing
   ========================================================================== */
function initEnquiryForm() {
    const enquiryForm = document.getElementById('enquiry-form');
    if (!enquiryForm) return;

    const responseContainer = document.getElementById('enquiry-response');

    enquiryForm.addEventListener('submit', (e) => {
        e.preventDefault();

        if (!validateForm(enquiryForm)) return;

        // Retrieve form fields
        const name = document.getElementById('fullname').value.trim();
        const service = document.getElementById('service-type').value;
        const urgency = document.getElementById('urgency').value;

        // Cost Calculation Logic
        let baseCost = 0;
        let serviceName = '';

        switch (service) {
            case 'bespoke-suit':
                baseCost = 3500;
                serviceName = 'Bespoke Suit Fitting & Tailoring';
                break;
            case 'wedding-groomsmen':
                baseCost = 8500;
                serviceName = 'Wedding Party Outfitting Package';
                break;
            case 'streetwear-bulk':
                baseCost = 1800;
                serviceName = 'Casual Streetwear Bulk Order';
                break;
            case 'footwear':
                baseCost = 1500;
                serviceName = 'Footwear & Accessories Order';
                break;
            default:
                baseCost = 500;
                serviceName = 'General Brand Consultation';
        }

        // Multiplier based on urgency
        let urgencyFee = 0;
        if (urgency === 'urgent') urgencyFee = 500;
        if (urgency === 'emergency') urgencyFee = 1200;

        const totalCost = baseCost + urgencyFee;

        // AJAX Submission Simulation
        submitViaAJAX({ name, service: serviceName, totalCost }, () => {
            responseContainer.style.display = 'block';
            responseContainer.className = 'response-card success';
            responseContainer.innerHTML = `
                <h3>Fitting Enquiry Received!</h3>
                <p>Thank you, <strong>${escapeHTML(name)}</strong>. We have processed your request for <strong>${serviceName}</strong>.</p>
                <div class="pricing-summary">
                    <p><strong>Estimated Base Cost:</strong> R${baseCost}.00</p>
                    <p><strong>Service/Urgency Fee:</strong> R${urgencyFee}.00</p>
                    <p class="grand-total"><strong>Estimated Total: R${totalCost}.00</strong></p>
                </div>
                <p>Our fitting master will contact you within 24 hours to confirm your appointment time.</p>
            `;
            enquiryForm.reset();
        });
    });
}

/* ==========================================================================
   4.2. Contact Form Logic & Dynamic Email Compilation
   ========================================================================== */
function initContactForm() {
    const contactForm = document.getElementById('contact-form');
    if (!contactForm) return;

    const responseContainer = document.getElementById('contact-response');

    contactForm.addEventListener('submit', (e) => {
        e.preventDefault();

        if (!validateForm(contactForm)) return;

        const name = document.getElementById('contact-name').value.trim();
        const email = document.getElementById('contact-email').value.trim();
        const phone = document.getElementById('contact-phone').value.trim();
        const subjectType = document.getElementById('message-type').value;
        const message = document.getElementById('contact-message').value.trim();

        const recipientEmail = "info@gutsandguys.co.za";
        const emailSubject = encodeURIComponent(`[${subjectType.toUpperCase()}] Inquiry from ${name}`);
        const emailBody = encodeURIComponent(
            `Name: ${name}\nEmail: ${email}\nPhone: ${phone}\nMessage Type: ${subjectType}\n\nMessage:\n${message}`
        );

        const mailtoURL = `mailto:${recipientEmail}?subject=${emailSubject}&body=${emailBody}`;

        submitViaAJAX({ name, email, subjectType }, () => {
            responseContainer.style.display = 'block';
            responseContainer.className = 'response-card success';
            responseContainer.innerHTML = `
                <h3>Message Compiled Successfully!</h3>
                <p>Thank you, <strong>${escapeHTML(name)}</strong>. Your message is ready to be sent to <strong>${recipientEmail}</strong>.</p>
                <a href="${mailtoURL}" class="btn btn-primary" target="_blank">Open Email Client to Send</a>
            `;
            contactForm.reset();
        });
    });
}

/* ==========================================================================
   Helper Validation Engine & Error Handling
   ========================================================================== */
function validateForm(form) {
    let isValid = true;
    const inputs = form.querySelectorAll('input[required], select[required], textarea[required]');

    inputs.forEach(input => {
        const errorElement = document.getElementById(`${input.id}-error`);
        let errorMessage = '';

        if (!input.value.trim()) {
            errorMessage = 'This field is required.';
            isValid = false;
        } else if (input.type === 'email' && !validateEmail(input.value)) {
            errorMessage = 'Please enter a valid email address.';
            isValid = false;
        } else if (input.type === 'tel' && !validatePhone(input.value)) {
            errorMessage = 'Please enter a valid 10-digit South African phone number.';
            isValid = false;
        }

        if (errorElement) {
            errorElement.innerText = errorMessage;
            errorElement.style.display = errorMessage ? 'block' : 'none';
        }

        if (errorMessage) {
            input.classList.add('input-error');
        } else {
            input.classList.remove('input-error');
        }
    });

    return isValid;
}

function validateEmail(email) {
    const re = /^[^\s@]+@[^\s@]+\.[^\s@]+$/;
    return re.test(email);
}

function validatePhone(phone) {
    const re = /^(\+27|0)[6-8][0-9]{8}$/;
    return re.test(phone.replace(/\s+/g, ''));
}

function submitViaAJAX(data, callback) {
    // Simulating AJAX Fetch Promise
    setTimeout(() => {
        callback();
    }, 400);
}

function escapeHTML(str) {
    return str.replace(/[&<>'"]/g, 
        tag => ({ '&': '&amp;', '<': '&lt;', '>': '&gt;', "'": '&#39;', '"': '&quot;' }[tag] || tag)
    );
}
