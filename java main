/**
 * GUTS & GUYS - Main JavaScript Enhancements (js/main.js)
 * Implements Accordions, Leaflet Interactive Map, Lightbox, and Dynamic Search/Filter
 */

document.addEventListener('DOMContentLoaded', () => {
    initAccordion();
    initLeafletMap();
    initLightbox();
    initDynamicSearch();
});

/* ==========================================================================
   2.1. Interactive Elements: Accordion Component
   ========================================================================== */
function initAccordion() {
    const accordionHeaders = document.querySelectorAll('.accordion-header');
    
    accordionHeaders.forEach(header => {
        header.addEventListener('click', () => {
            const accordionItem = header.parentElement;
            const accordionContent = header.nextElementSibling;

            // Toggle Active Class
            const isActive = accordionItem.classList.contains('active');
            
            // Close all items
            document.querySelectorAll('.accordion-item').forEach(item => {
                item.classList.remove('active');
                item.querySelector('.accordion-content').style.maxHeight = null;
            });

            // If it wasn't active, open it
            if (!isActive) {
                accordionItem.classList.add('active');
                accordionContent.style.maxHeight = accordionContent.scrollHeight + 'px';
            }
        });
    });
}

/* ==========================================================================
   2.1. Interactive Elements: Leaflet.js Interactive Map
   ========================================================================== */
function initLeafletMap() {
    const mapElement = document.getElementById('store-map');
    if (!mapElement) return;

    // Polokwane Central Coordinates
    const storeCoordinates = [-23.9045, 29.4217];

    // Initialize map
    const map = L.map('store-map').setView(storeCoordinates, 15);

    // Tile Layer (OpenStreetMap)
    L.tileLayer('https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png', {
        maxZoom: 19,
        attribution: '&copy; <a href="https://www.openstreetmap.org/copyright">OpenStreetMap</a> contributors'
    }).addTo(map);

    // Custom Marker
    const marker = L.marker(storeCoordinates).addTo(map);
    marker.bindPopup(`
        <strong>GUTS & GUYS Boutique & Studio</strong><br>
        45 Market Street, Polokwane Central<br>
        <em>Open Today: 08:00 - 17:00</em>
    `).openPopup();
}

/* ==========================================================================
   2.1. Interactive Elements: Lightbox Gallery
   ========================================================================== */
function initLightbox() {
    const galleryImages = document.querySelectorAll('.lightbox-trigger');
    const lightboxModal = document.getElementById('lightbox-modal');
    if (!lightboxModal) return;

    const lightboxImg = document.getElementById('lightbox-img');
    const lightboxCaption = document.getElementById('lightbox-caption');
    const closeBtn = document.querySelector('.lightbox-close');

    galleryImages.forEach(img => {
        img.addEventListener('click', () => {
            lightboxModal.style.display = 'block';
            lightboxImg.src = img.src;
            lightboxCaption.innerText = img.alt || 'GUTS & GUYS Apparel Collection';
        });
    });

    if (closeBtn) {
        closeBtn.addEventListener('click', () => {
            lightboxModal.style.display = 'none';
        });
    }

    // Close on outside click
    lightboxModal.addEventListener('click', (e) => {
        if (e.target === lightboxModal) {
            lightboxModal.style.display = 'none';
        }
    });
}

/* ==========================================================================
   2.2. Dynamic Content & Search/Filter Functionality
   ========================================================================== */
function initDynamicSearch() {
    const searchInput = document.getElementById('catalogue-search');
    const categoryFilter = document.getElementById('category-filter');
    const items = document.querySelectorAll('.searchable-item');

    if (!searchInput && !categoryFilter) return;

    function filterItems() {
        const query = searchInput ? searchInput.value.toLowerCase().trim() : '';
        const selectedCategory = categoryFilter ? categoryFilter.value.toLowerCase() : 'all';

        items.forEach(item => {
            const title = item.querySelector('.item-title')?.innerText.toLowerCase() || '';
            const description = item.querySelector('.item-desc')?.innerText.toLowerCase() || '';
            const category = item.dataset.category ? item.dataset.category.toLowerCase() : '';

            const matchesQuery = title.includes(query) || description.includes(query);
            const matchesCategory = selectedCategory === 'all' || category === selectedCategory;

            if (matchesQuery && matchesCategory) {
                item.style.display = '';
            } else {
                item.style.display = 'none';
            }
        });
    }

    if (searchInput) searchInput.addEventListener('input', filterItems);
    if (categoryFilter) categoryFilter.addEventListener('change', filterItems);
}
