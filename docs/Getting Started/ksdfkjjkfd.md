---
title: ksdfkjjkfd
deprecated: false
hidden: false
metadata:
  robots: index
---
<HTMLBlock>
  {`
  <style>
    .dropdown-menu {
      font-family: Arial, sans-serif;
      max-width: 250px;
      margin-left: auto; 
      margin-right: 0; 
      border: 1px solid #ddd;
      border-radius: 8px;
      padding: 10px;
      background: #4A4AF4;
      overflow: hidden; 
    }
    .dropdown-item {
      margin-bottom: 10px;
    }
    .dropdown-toggle {
      display: block;
      width: 100%;
      text-align: left;
      padding: 10px;
      background: #fff;
      border: 1px solid #ddd;
      border-radius: 4px;
      cursor: pointer;
    }
    .dropdown-toggle:hover {
      background: #f0f0f0;
    }
    .dropdown-content {
      display: none;
      margin-top: 5px;
      padding: 10px;
      background: #fff;
      border: 1px solid #ddd;
      border-radius: 4px;
    }
    .dropdown-item.open .dropdown-content {
      display: block;
    }
    .flag-icon {
      width: 20px;
      height: 20px;
      margin-right: 10px;
    }
    .product-item {
      margin-bottom: 5px;
    }
    .product-icon {
      width: 20px;
      height: 20px;
      margin-right: 10px;
    }
    .country-title {
      font-family: Arial, sans-serif;
      font-size: 20px;
      text-align: center;
      font-weight: bold;
      color: #ffffff;
    } 
  </style>

  <div class="dropdown-menu">
    <p class="country-title">Country Availability</p>
    <div class="dropdown-item" id="country-dropdown">
      <button class="dropdown-toggle" onclick="toggleDropdown(event)">
        <b>Country List</b> ⬇️
      </button>
      <div class="dropdown-content">
        <div class="product-item">
          <img src="https://files.readme.io/a4c8b3d6596d943e2b93c82cb1d432a2edaf6998667835c2e97ef4a31d460c7e-us-circle-01.png" alt="USA" class="flag-icon" />
          USA
        </div>
        <div class="product-item">
          <img src="https://files.readme.io/3ca294a1b4b8b8506c3ff32876abc6e3e33d0e65a509dab81398915094bdbc5c-61TcZ33ZrJL._AC_UY1000_.jpg" alt="Canada" class="flag-icon" />
          Canada
        </div>
        <div class="product-item">
          <img src="https://files.readme.io/db98461fef617df7c9970e98f01150f067fcee1fc823a450f09056138b9f70be-united-kingdom-flag-rounded-icon-uk-flag-union-jack-vector.jpg" alt="UK" class="flag-icon" />
          UK
        </div>
      </div>
    </div>
  </div>


  `}
</HTMLBlock>