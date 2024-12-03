# Shopify Checkout Header Customization

This repository contains the code for customizing the checkout header in Shopify using GraphQL and Shopify UI Extensions.

## Overview
Shopify allows merchants to customize their checkout flow, and with this extension, we are customizing the header section to hide the default back-to-cart icon and the buyer journey breadcrumbs. Additionally, we have replaced the default checkout header with a custom extension.

## Features
- **GraphQL Queries**: Fetch checkout profiles and apply branding customizations.
- **Checkout UI Extension**: Modify the header with a custom extension to display buyer journey steps and cart link.
- **Customization**: Ability to hide default elements like back-to-cart and breadcrumbs and replace them with custom elements.

## Steps
1. **Fetching Checkout Profile ID**:
    The first step is to use a GraphQL query to fetch the checkout profile ID, which helps in identifying the active checkout profile on the live store.

    ```graphql
    query checkoutProfiles {
      checkoutProfiles(first: 1, query: "is_published:true") {
        edges {
          node {
            id
            name
          }
        }
      }
    }
    ```

2. **Updating Checkout Branding**:
    Once we have the checkout profile ID, we proceed to update the checkout branding to hide the default back-to-cart icon and buyer journey breadcrumbs.

    ```graphql
    mutation updateCheckoutBranding($checkoutBrandingInput: CheckoutBrandingInput!, $checkoutProfileId: ID!) {
      checkoutBrandingUpsert(checkoutBrandingInput:$checkoutBrandingInput, checkoutProfileId:$checkoutProfileId) {
        checkoutBranding {
          customizations {
            buyerJourney {
              visibility
            }
            cartLink {
              visibility
            }
          }
        }
      }
    }
    ```

3. **Creating a Custom Extension for Checkout Header**:
    - We use `@shopify/ui-extensions-react` to create a custom extension that replaces the default header and displays custom breadcrumbs.

4. **Customization File Structure**:
    - **Extension.jsx**: Contains the logic for rendering the custom header and buyer journey steps.
    - **shopify.extension.toml**: Configuration file for defining extension details and targeting checkout header.

## Requirements
- Shopify Partner Account
- Shopify store access with permission to modify checkout and extensions.
- Knowledge of GraphQL and Shopify UI Extensions.

## Setup
1. Clone this repository to your local machine.
2. Install required dependencies using `npm` or `yarn`.
3. Deploy the extension to your Shopify store using the CLI.

## License
This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.
