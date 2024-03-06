<script lang="ts">
    let distance = 55;
    let fuelPrice = 1.93;
    let cityConsumption = 13.2;
    let highwayConsumption = 20.4;

    function formatPrice(price: number) {
        return Intl.NumberFormat('nl-NL', { style: 'currency', currency: 'EUR' }).format(price);
    }

    function formatConsumption(volume: number) {
        return Math.round(volume * 100) / 100;
    }

// Dus 146km wil je in totaal rijden.

// De auto rijd in de stad 1 liter op 13.2km. 

// Dus 146km / 13,2km = 11 liter brandstof

// 11 liter x 1,93eu (brandstof prijs) = 21,23eu

// Deze zelfde som maar dan met optimaal verbruik, namelijk _Vebruik snelweg_:

// Dus 146km / 20,4km = 7,15 liter brandstof

// 7,15 liter x 1,93eu (brandstof prijs) = 13,81eu


// De totale brandstofkosten liggen dus tussen de 21,23eu (max verbruik) en 13,81eu (min verbruik). Dat komt dan gemiddeld uit op 21,23 + 13,81 / 2 = 17,52eu
</script>

<section>
    <form>
        <legend>Calculate fuel cost</legend>
        <div>
            <label for="distance">Distance</label>
            <input type="number" bind:value={distance} min="0" step="1" />
        </div>
            <div>
            <label for="fuelPrice">Fuel price</label>
            <input type="number" bind:value={fuelPrice} min="0" step="0.01" />
        </div>
        <div>
            <label for="cityConsumption">City consumption</label>
            <input type="number" bind:value={cityConsumption} min="0" step="0.1" />
        </div>
        <div>
            <label for="highwayConsumption">Highway consumption</label>
            <input type="number" bind:value={highwayConsumption} min="0" step="0.1" />
        </div>
    </form>
</section>

<section>
    <h2>Fuel consumption</h2>
    <p>City consumption: {formatConsumption(distance / cityConsumption)} liters</p>
    <p>Highway consumption: {formatConsumption(distance / highwayConsumption)} liters</p>
    <p>Average consumption: {formatConsumption((distance / cityConsumption + distance / highwayConsumption) / 2)} liters</p>
    <h2>Cost comparison</h2>
    <p>City fuel cost: {formatPrice(distance / cityConsumption * fuelPrice)}</p>
    <p>Highway fuel cost: {formatPrice(distance / highwayConsumption * fuelPrice)}</p>
    <p>Average fuel cost: {formatPrice(((distance / cityConsumption * fuelPrice) + (distance / highwayConsumption * fuelPrice)) / 2)}</p>
</section>
